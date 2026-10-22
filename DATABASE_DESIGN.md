# Database Design

Claude must implement this design through timestamped Supabase migrations. Do not create production-only tables manually through the dashboard.

## Extensions and conventions

- UUID primary keys generated in PostgreSQL.
- `timestamptz` for timestamps.
- UTC storage.
- `created_at` and `updated_at` on mutable business entities.
- Database constraints for status, price and sort-order validity.
- Trigger or explicit application logic to maintain `updated_at`.
- Slugs and product codes case-insensitively unique where appropriate.

## `admin_profiles`

| Column | Notes |
|---|---|
| `id` | UUID PK; normally same value as Auth user ID |
| `full_name` | Required |
| `role` | `super_admin` or `content_admin` |
| `is_active` | Defaults false until approved |
| `invitation_status` | `pending`, `accepted`, `expired` or `revoked` as needed |
| `created_at` | Timestamp |
| `updated_at` | Timestamp |

Do not expose email from Auth through a public table.

## `admin_invitations`

| Column | Notes |
|---|---|
| `id` | UUID PK |
| `email_normalized` | Lowercase; visible only to super admins |
| `full_name` | Intended administrator name |
| `role` | Requested role |
| `status` | `pending`, `accepted`, `expired`, `revoked` |
| `invited_by` | Super-admin UUID |
| `auth_user_id` | Nullable until accepted |
| `expires_at` | Timestamp |
| audit columns | created/updated timestamps |

Do not store invitation tokens. Supabase Auth owns the actual invitation secret.

## `categories`

| Column | Notes |
|---|---|
| `id` | UUID PK |
| `name` | Required |
| `slug` | Unique, URL-safe |
| `description` | Optional |
| `image_path` | Optional Supabase Storage path |
| `is_featured` | Default false |
| `is_active` | Default true |
| `sort_order` | Non-negative integer |
| `seo_title` | Optional |
| `seo_description` | Optional |
| audit columns | created/updated/by |

## `products`

| Column | Notes |
|---|---|
| `id` | UUID PK |
| `product_code` | Unique business reference |
| `name` | Required |
| `slug` | Unique |
| `short_description` | Required for publication |
| `description` | Required for publication |
| `product_type` | Ring, earrings, etc. |
| `collection_name` | Optional |
| `price_display_type` | `as_shown`, `on_request`, `from` |
| `indicative_price_minor` | Integer minor units; nullable |
| `currency` | Default `INR` |
| `made_to_order` | Default true |
| `status` | `draft`, `published`, `archived` |
| `is_featured` | Default false |
| `is_new_arrival` | Default false |
| `materials` | JSONB string array |
| `stone_details` | JSONB structured data or text per final design |
| `configuration_details` | JSONB |
| `customisation_details` | Text |
| `lead_time` | Text |
| `certification_details` | Text |
| `whatsapp_message` | Optional override |
| `seo_title` | Optional |
| `seo_description` | Optional |
| `sort_order` | Non-negative integer |
| `published_at` | Set on publication |
| audit columns | created/updated/by |

Store money as integer minor units, never floating point.

## `product_colour_variants`

| Column | Notes |
|---|---|
| `id` | UUID PK |
| `product_id` | FK |
| `gold_colour` | `yellow_gold`, `white_gold`, `rose_gold` |
| `display_label` | Customer-visible label |
| `swatch_hex` | Validated visual token; never the only indicator |
| `is_default` | Exactly one enabled default per publishable product |
| `is_active` | Availability flag |
| `price_override_minor` | Optional colour-specific displayed price |
| `configuration_details` | JSONB/text for colour-specific information |
| `sort_order` | Non-negative integer |
| audit columns | created/updated/by |

Unique: `product_id`, `gold_colour`. Enforce at most one default using a partial unique index; publication validation enforces exactly one.

## `product_categories`

- Composite PK: `product_id`, `category_id`.
- Foreign keys with deliberate delete behaviour.
- Index both directions.

## `product_images`

| Column | Notes |
|---|---|
| `id` | UUID PK |
| `product_id` | FK |
| `colour_variant_id` | Nullable FK; null means shared/general image |
| `storage_path` | Required and unique |
| `alt_text` | Required before product publication |
| `is_primary` | Only one primary image per product |
| `sort_order` | Non-negative |
| `created_at` | Timestamp |
| `created_by` | Admin UUID |

Enforce one primary image per colour variant and one shared primary image per product with partial unique indexes where supported.

Storefront image fallback order: selected variant primary → shared primary → first selected-variant image → first shared image → branded placeholder.

## `site_settings`

Prefer a single validated row or controlled key/value design. Required values include brand name, contact details, WhatsApp settings, social URLs and default SEO data. Avoid arbitrary executable HTML.

## `page_sections`

- `id`
- `page_key`
- `section_key`
- `heading`
- `body`
- `image_path`
- `configuration` JSONB for controlled presentation values
- `is_visible`
- `sort_order`
- audit columns

Unique: `page_key`, `section_key`.

## `homepage_carousel_slides`

| Column | Notes |
|---|---|
| `id` | UUID PK |
| `eyebrow` | Optional short label |
| `heading` | Required |
| `supporting_text` | Optional, length limited |
| `desktop_image_path` | Required before publication |
| `mobile_image_path` | Required before publication |
| `image_alt_text` | Required before publication |
| `desktop_focal_x/y` | Validated 0–100 percentages |
| `mobile_focal_x/y` | Validated 0–100 percentages |
| `primary_cta_label/url` | Required label and validated destination |
| `secondary_cta_label/url` | Optional pair; both or neither |
| `status` | `draft`, `published`, `archived` |
| `starts_at` / `ends_at` | Optional schedule; end must follow start |
| `sort_order` | Non-negative integer |
| audit columns | created/updated/by and published timestamp |

Anonymous users may read only currently published, currently scheduled slides. Active administrators manage drafts. Do not store arbitrary HTML or executable URLs.

## `audit_log` — recommended

- Administrator
- Action
- Entity type/ID
- Safe old/new value snapshot
- Timestamp

Never log passwords, sessions, tokens or private Auth payloads.

## Seed data

Seed:

- Draft categories
- One draft example product
- Placeholder site settings
- Placeholder page sections

Never seed fake public phone numbers or email addresses. Seed content remains draft/hidden until business values are supplied.

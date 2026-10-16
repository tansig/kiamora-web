# Kiamora Website and Admin Portal Specification

## 1. Objective

Build a premium, responsive storefront for Kiamora, a bespoke jewellery brand, together with a secure administrative portal that allows Kiamora staff to manage products, categories, images and configurable website content without changing source code.

## 2. Business model

- Designs are starting points for bespoke orders.
- Products may show the price of the displayed configuration.
- The customer can request changes to stone, metal, purity, size, engraving and other details.
- Kiamora confirms the final price after consultation.
- The website does not accept payment or create confirmed orders.
- WhatsApp is the primary conversion channel.

Required price clarification:

```text
As shown: ₹85,000

This is the price of the displayed configuration. Your final quotation will
reflect your selected stones, metal, size and personalisation.
```

## 3. Public routes

- `/` homepage
- `/collections`
- `/collections/[slug]`
- `/products/[slug]`
- `/bespoke`
- `/about`
- `/guide`
- `/faq`
- `/contact`
- `/privacy-policy`
- `/terms`
- `/shipping`
- `/cancellation-and-returns`
- `/jewellery-care`
- custom 404

## 4. Administrative routes

- `/admin/login`
- `/admin`
- `/admin/products`
- `/admin/products/new`
- `/admin/products/[id]/edit`
- `/admin/categories`
- `/admin/media`
- `/admin/homepage`
- `/admin/pages`
- `/admin/settings`
- `/admin/profile`

All admin routes except login and auth callback require an authenticated, active administrator.

## 5. Public customer journey

1. Discover Kiamora.
2. Browse or filter designs.
3. Open a product.
4. Review configuration and `As shown` price.
5. Select or describe desired customisation.
6. Choose `Customise This Design`.
7. Continue in WhatsApp with a pre-filled product-specific message.
8. Receive a final quotation from Kiamora.

## 6. Homepage

- Announcement strip
- Header/navigation
- Premium hero
- Featured categories
- Featured products
- Bespoke proposition/process
- Kiamora story
- Craftsmanship/quality section
- Approved testimonials only
- Social link section
- Consultation CTA
- Footer

Default direction: deep green, ivory and restrained gold; elegant serif display type; clean sans-serif body type; generous whitespace; diamond-present Kiamora emblem.

## 7. Catalogue and product page

- Server-rendered public product/category data.
- Search and filters by name, reference, category and collection.
- Product cards with image, name, category, price status and badges.
- Draft/archived products excluded from all public pages and sitemap.
- Product gallery, configuration, story, customisation, delivery, certification and related designs.
- Accessible, URL-encoded WhatsApp action.

## 8. Admin capability

- Invite-only login/logout/reset password.
- Dashboard summary.
- Product create, edit, duplicate, preview, publish, unpublish, archive and restore.
- Category create/edit/activate/deactivate/reorder.
- Multiple product-category assignments.
- Image upload, alt text, primary selection, reorder and safe deletion.
- Featured products/categories and sort order.
- Homepage and selected editorial content editing.
- Business/contact/default SEO settings.
- Clear confirmation for destructive actions.

Detailed behaviour is in `ADMIN_REQUIREMENTS.md`.

## 9. Architecture

- Astro SSR + TypeScript.
- React for interactive admin components.
- Cloudflare adapter and Cloudflare Workers.
- Supabase PostgreSQL, Auth and Storage.
- Version-controlled SQL migrations.
- RLS on every exposed table.
- Public image reads; administrator-only image writes.
- Environment-specific configuration.

## 10. Content states

Products use:

- `draft`
- `published`
- `archived`

Only `published` products are visible publicly. Categories require `is_active = true` to be public.

## 11. SEO and quality

- Unique title and description.
- Canonical URLs.
- Open Graph/social metadata.
- Sitemap and robots.
- Organisation and Product JSON-LD.
- Descriptive alt text.
- Responsive at 390px, 768px and 1440px.
- Keyboard accessible and usable without a mouse.
- No critical console errors.
- Core public pages usable with JavaScript failure where practical.

## 12. Placeholders

- Missing text begins with `[CONTENT REQUIRED]` in seed data.
- Fake phone numbers and email addresses must not be published.
- Draft legal wording must be visibly marked for approval.
- AI-generated jewellery must not be represented as a real Kiamora product without approval.
- Missing content is tracked in `CONTENT_PENDING.md`.

## 13. Explicitly out of scope for MVP

- Cart and checkout
- Payment gateway
- Customer accounts
- Inventory/order management
- Live gold-rate pricing
- Automatic quotation calculation
- PDF quotation generation
- AR try-on
- CRM
- Drag-and-drop page builder
- Bulk spreadsheet import
- Multi-tenant functionality

## 14. Completion criteria

- Authorised administrator can manage products, categories, images and basic content.
- Anonymous and unauthorised writes fail.
- Published changes appear on the public storefront without source changes.
- Draft/archived data remains private.
- Browse → product → WhatsApp journey works.
- All documented automated checks pass.
- Preview deployment succeeds.
- Manual security and responsive checks pass.
- Handover documentation is usable by a non-developer administrator.

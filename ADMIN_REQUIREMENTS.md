# Administrative Portal Requirements

## 1. Authentication

- Email/password login through Supabase Auth.
- No public sign-up screen.
- Password reset through approved redirect URLs.
- Server-side route protection.
- Active admin profile check after authentication.
- Friendly messages without revealing whether an email exists.
- Logout invalidates the local session and returns to login.

## 2. Dashboard

Show:

- Total, published, draft and archived products
- Active/inactive categories
- Products without a primary image
- Products missing key content
- Recently updated products

Quick actions: Add Product, Add Category, Edit Homepage, View Storefront.

## 3. Product editor

Required fields:

- Product code/reference
- Name
- Slug
- Short description
- Full description
- Status
- At least one category before publication
- Price display type
- Primary image before publication

Optional/configurable fields:

- Collection
- Indicative/displayed price
- Product type
- 14K/18K/platinum availability
- Gold colours
- Natural/lab-grown/gemstone information
- Weight/configuration details
- Customisation options
- Lead time
- Certification text
- Featured/new-arrival flags
- Manual sort order
- SEO title/description
- Custom WhatsApp message

Actions:

- Save draft
- Preview
- Publish
- Unpublish
- Duplicate
- Archive
- Restore

Publishing validation must be stricter than draft validation.

## 4. Category editor

- Name and unique slug
- Description
- Hero/card image
- Active and featured flags
- Sort order
- SEO title/description
- Product count

Warn before deactivation. Block permanent deletion when products are assigned unless assignments are explicitly resolved.

## 5. Media

- JPEG, PNG, WebP and AVIF input.
- Maximum source upload 5 MB.
- Validate MIME type, not only extension.
- Sanitised unique storage path.
- Preview, alt text, primary image and ordering.
- Warn before deleting an in-use object.
- Prefer WebP/AVIF and a target delivery size below 400 KB.

## 6. Homepage/content editor

Editable settings:

- Announcement
- Hero heading/subheading/image
- Primary/secondary CTA labels and links
- Featured categories/products
- Bespoke intro
- About preview
- Consultation CTA
- Section visibility

Provide structured fields, not unrestricted HTML.

## 7. Business settings

- Brand name
- WhatsApp number
- Email and phone
- Address/service area
- Business hours
- Social URLs
- Default WhatsApp message
- Default SEO title/description
- Currency and price-display policy

## 8. UX requirements

- Responsive at laptop and tablet widths.
- Clear saving/success/error states.
- Prevent accidental double submit.
- Unsaved-change warning.
- Confirmation dialog for archive/delete.
- Accessible labels and validation messages.
- Never show secret configuration in the UI.

# Kiamora UI Specifications

These specifications govern both the public storefront and administrative portal. The files under `mockups/` are visual references, not screenshots of finished software.

## 1. Technology and rendering

- Angular 22.x latest stable patch at project creation.
- Standalone components only; do not introduce NgModules without a documented integration need.
- Strict TypeScript and typed reactive/signal forms.
- Signals for local UI state and derived view state.
- Route-level lazy loading.
- Angular hybrid rendering:
  - SSR: homepage, collections, catalogue and product details.
  - Prerender: suitable stable policy/editorial routes.
  - CSR: authenticated admin experience after the protected shell loads.
- Hydration enabled for SSR routes.
- Angular Material 3/CDK may supply accessible admin primitives, overlays, dialogs, menus, tables, drag/drop and focus management.
- Storefront must use custom Kiamora components rather than looking like a default Material application.

## 2. Brand system

### Colours

| Token | Value | Use |
|---|---:|---|
| `--km-forest-950` | `#082A24` | Storefront header, admin sidebar |
| `--km-forest-900` | `#0D3B32` | Primary surfaces/actions |
| `--km-forest-700` | `#1F5C4D` | Secondary emphasis |
| `--km-gold-500` | `#C6A66B` | Luxury accent |
| `--km-gold-300` | `#E2CF9F` | Borders/highlights |
| `--km-ivory-50` | `#FBF8F1` | Main storefront canvas |
| `--km-stone-100` | `#F2EFE7` | Soft surfaces |
| `--km-ink-900` | `#1D2522` | Primary text |
| `--km-ink-600` | `#65706C` | Supporting text |
| `--km-success` | `#23845F` | Success/published |
| `--km-warning` | `#C8872D` | Warning/draft |
| `--km-danger` | `#B54747` | Destructive/error |

Meet WCAG AA contrast for normal text and controls. Gold is an accent, not the sole foreground for small text.

### Typography

- Display/headings: `Cormorant Garamond` or approved equivalent.
- UI/body: `Manrope` or approved equivalent.
- Use locally hosted or privacy-reviewed web fonts; provide reliable fallbacks.
- Storefront H1: 52–68px desktop, 38–44px mobile.
- Admin page title: 28–32px.
- Body: 16px storefront; 14–16px admin.

### Shape and elevation

- Storefront: 0–8px radius, restrained borders, minimal shadow.
- Admin: 10–14px cards, one subtle shadow level.
- Buttons: 8px radius admin; near-square or 4px luxury storefront treatment.
- Focus ring: clearly visible 2px forest/gold combination.

## 3. Responsive grid

| Breakpoint | Behaviour |
|---|---|
| `< 600px` | Single-column storefront; admin list cards replace wide tables where necessary |
| `600–959px` | Tablet; 2-column catalogue; collapsible admin sidebar |
| `960–1279px` | Desktop; fixed admin sidebar; 3-column catalogue |
| `>= 1280px` | Wide desktop; max content width 1440px; 4-column catalogue where appropriate |

Minimum tap target: 44×44px. No horizontal page scrolling at 390px.

## 4. Public storefront shell

### Header

- Optional announcement bar.
- Diamond-present Kiamora emblem and wordmark.
- Navigation: New, Rings, Earrings, Necklaces, Bespoke, About.
- Search and WhatsApp/consultation actions.
- Sticky only when it does not obstruct product imagery.

### Product detail layout

Desktop:

- Left 58%: gallery with one main image and selectable thumbnails.
- Right 42%: breadcrumbs, collection, title, reference, price, colour selector, details and CTA.
- Information column remains visible while browsing images where practical.

Mobile:

- Swipeable gallery first.
- Product information below.
- Sticky bottom `Customise on WhatsApp` action after selection.

### Gold-colour selector

Options may include:

- Yellow Gold — swatch `#D6B768`
- White Gold — swatch `#D8D8D3`
- Rose Gold — swatch `#C9907D`

Every option displays swatch plus text. Selected state uses a 2px outline, check mark and `aria-pressed`/radio semantics. Unavailable variants are disabled with explanatory text.

On selection:

1. Update gallery to that variant's ordered images.
2. Update displayed price if a variant override exists.
3. Update configuration copy.
4. Retain keyboard focus.
5. Include colour in WhatsApp message.
6. Optionally reflect selection in the URL query string for sharing.

Show a polite fallback notice only to administrators/preview users when colour-specific imagery is missing; customers see the shared gallery without an error.

### Product gallery

- Preserve image aspect ratio.
- Thumbnail has visible selected state.
- Keyboard navigation and descriptive alt text.
- Zoom/lightbox optional for MVP but must be accessible if added.
- Changing colour must not cause severe layout shift.

## 5. Admin application shell

### Navigation

Left navigation on desktop:

- Dashboard
- Products
- Categories
- Media
- Homepage
- Pages
- Administrators — super admin only
- Settings

Bottom: View Storefront, current admin profile, Log out.

Tablet/mobile uses a top bar plus drawer. Preserve the active route and focus behaviour.

### Top bar

- Page title/breadcrumb.
- Optional global search.
- Notifications limited to useful system/content warnings.
- User avatar/menu.

### Standard admin page anatomy

1. Breadcrumb/title and primary action.
2. Optional summary/help text.
3. Filters/search.
4. Main list/editor.
5. Clear empty/loading/error state.

## 6. Admin dashboard

- KPI cards: All Products, Published, Draft, Categories.
- Content-health panel: missing images, missing descriptions, unpublished changes.
- Recent-products table with status, colour count, updated date and actions.
- Quick actions.
- Avoid decorative charts without decision value.

## 7. Product editor

Desktop uses a 12-column layout:

- Main editor: 8 columns.
- Publish/summary rail: 4 columns.

Sections:

1. Basics
2. Categories/collection
3. Pricing/configuration
4. Gold colours and images
5. Bespoke details
6. SEO

### Colour and image editor

- Toggle cards for Yellow/White/Rose Gold.
- Enabled colours create labelled tabs.
- Each tab contains a sortable image grid.
- Image card: preview, primary badge, alt-text status, reorder handle and overflow menu.
- `Upload images` supports multiple files and progress.
- `Set as default colour` is explicit.
- Publication summary shows missing requirements per colour.

### Publish rail

- Status badge.
- Save draft.
- Preview.
- Publish/unpublish.
- Archive in secondary/destructive area.
- Last modified/by.
- Disable Publish until required validation passes and explain every issue.

## 8. Administrator users screen

Only super admins can route or query this feature.

### List

Columns:

- Name/email
- Role
- Status
- Invited/created date
- Last sign-in
- Actions

Status values: Invitation Pending, Active, Inactive, Expired.

### Invite drawer/dialog

Fields:

- Full name
- Email
- Role

Explain permissions before submission. Confirmation shows that an invitation was sent; never show a password.

### Row actions

- Resend invite
- Change role
- Deactivate/activate
- Revoke pending invitation

Destructive/privilege changes require confirmation. Block any action that leaves zero active super admins.

## 9. Forms and feedback

- Persistent labels; placeholders never replace labels.
- Inline errors beside fields plus top summary for long forms.
- Dirty-form navigation guard.
- Save button shows progress and prevents duplicate submission.
- Toast for concise confirmation; important errors remain inline.
- Skeleton loading only when layout is known; use progress indicators for mutations.

## 10. Accessibility

- WCAG 2.2 AA target.
- Logical heading structure and landmarks.
- Full keyboard operation.
- Focus returned correctly after dialogs/drawers.
- Accessible names for icon-only controls.
- No state communicated only with colour.
- Reduced-motion support.
- Screen-reader announcement for gallery colour changes, uploads and save results.

## 11. Screen/component mapping

| Route | Primary Angular components |
|---|---|
| `/products/:slug` | ProductGallery, GoldColourSelector, ProductConfiguration, WhatsAppCta |
| `/admin` | AdminShell, MetricCard, ContentHealth, RecentProducts |
| `/admin/products/:id/edit` | ProductForm, ColourVariantEditor, VariantImageGrid, PublishPanel |
| `/admin/users` | AdminUserTable, InviteAdminDialog, RoleDialog, UserStatusDialog |

Use feature folders and route-level lazy loading. Keep Supabase access behind typed services/repositories; components do not contain raw queries.

## 12. Supplied visual references

- `mockups/storefront-product-colour-selection.svg/png`
- `mockups/admin-dashboard.svg/png`
- `mockups/admin-product-colour-images.svg/png`
- `mockups/admin-users.svg/png`

Implementation must match the hierarchy, density, palette and interaction intent—not blindly reproduce placeholder content or pixel coordinates.

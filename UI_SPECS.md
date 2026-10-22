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

The public storefront uses warm editorial neutrals from the approved homepage direction. Deep forest is retained for the administrative portal so operational screens remain clearly distinct from customer-facing luxury content.

| Token | Value | Use |
|---|---:|---|
| `--km-espresso-950` | `#241712` | Storefront dark bands, overlays and primary luxury actions |
| `--km-espresso-800` | `#3A2920` | Storefront headings and icon strokes |
| `--km-champagne-500` | `#A98245` | Storefront luxury accent |
| `--km-champagne-100` | `#E9DFCF` | Editorial feature surfaces |
| `--km-forest-950` | `#082A24` | Admin sidebar |
| `--km-forest-900` | `#0D3B32` | Admin primary surfaces/actions |
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

- Storefront: 0–4px radius, restrained borders, minimal shadow and image-led hierarchy.
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

- Slim announcement bar for consultation/service messaging.
- Diamond-present Kiamora emblem and wordmark.
- Navigation: New In, Rings, Earrings, Necklaces, Collections, Bespoke and Our Story.
- Search, profile and saved/bag-style enquiry affordances. A bag icon must not imply checkout in the MVP; it may be omitted or represent a saved enquiry list only.
- Desktop navigation may open an accessible image-led mega menu. Mobile uses a full-height drawer.
- Header may become sticky after the hero, but must not obstruct product imagery or cause layout shift.

### Homepage composition

The homepage is a premium editorial journey, not a generic grid of cards. It takes structural inspiration from mature jewellery commerce—fast discovery, collection storytelling, trust and consultation—while using only original Kiamora assets, content and code.

Required order:

1. Announcement strip and global header.
2. Full-width carousel with 2–5 slides.
3. Brand manifesto/intro statement.
4. Image-led category discovery.
5. Signature collection editorial split.
6. Trending/featured products.
7. Kiamora assurance/trust strip.
8. Private consultation/WhatsApp conversion panel.
9. Structured footer.

### Homepage carousel

- Minimum desktop visual height: 620px at 1440px viewport; mobile visual height 520–640px depending on copy.
- Every slide has separate desktop and mobile images, eyebrow, headline, optional supporting copy, primary CTA and optional secondary CTA.
- Admins set image focal points so crops preserve the jewellery and face/hands.
- Controls: previous/next arrows, slide dots, keyboard arrows and touch swipe.
- Autoplay default: six seconds. Pause on pointer hover, keyboard focus, page invisibility and reduced-motion preference.
- Do not autoplay video in the MVP.
- Text must meet WCAG AA over a deliberate overlay; never depend on the underlying photo remaining dark.
- First slide image is prioritised for LCP; later slides are lazy loaded. Avoid cumulative layout shift.
- Carousel content must be database driven, publishable/schedulable and previewable from `/admin/homepage`.

### Category, editorial and product modules

- Category cards are image-led with concise names and no paragraph overlays.
- Editorial split modules pair one strong image with one short narrative and a single CTA.
- Product rows show a maximum of four cards on wide desktop and two on mobile; horizontal scroll is allowed only with clear affordance.
- Wishlist/saved icons require accessible labels. Do not add cart or checkout behaviour.
- Trust claims must be approved and evidence-backed; placeholders remain hidden in production.

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

## 8.1 Homepage and carousel editor

Route: `/admin/homepage`.

- Tabs: Carousel, Sections and SEO.
- Carousel list supports add, duplicate, reorder, enable/disable, schedule and delete with confirmation.
- Each slide requires desktop image, mobile image, meaningful alt text, focal point, headline and valid internal/external CTA.
- Preview desktop and mobile crops before publishing.
- Show validation for contrast, missing responsive images, broken links and unavailable referenced categories/products.
- Configure autoplay and interval within safe bounds; reduced-motion behaviour cannot be disabled.
- Section editor controls visibility, order and references to featured categories/products without unrestricted HTML.
- Publishing is atomic: incomplete changes remain draft and do not replace the currently published homepage.

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
| `/` | StorefrontHeader, HeroCarousel, BrandManifesto, CategoryDiscovery, SignatureEditorial, FeaturedProducts, AssuranceStrip, ConsultationCta, StorefrontFooter |
| `/collections/:slug` | CollectionHero, CatalogueToolbar, FilterDrawer, ProductGrid, ProductCard |
| `/products/:slug` | ProductGallery, GoldColourSelector, ProductConfiguration, WhatsAppCta |
| `/admin` | AdminShell, MetricCard, ContentHealth, RecentProducts |
| `/admin/products/:id/edit` | ProductForm, ColourVariantEditor, VariantImageGrid, PublishPanel |
| `/admin/homepage` | HomepageEditor, CarouselSlideList, CarouselSlideForm, ResponsivePreview, SectionOrderEditor |
| `/admin/users` | AdminUserTable, InviteAdminDialog, RoleDialog, UserStatusDialog |

Use feature folders and route-level lazy loading. Keep Supabase access behind typed services/repositories; components do not contain raw queries.

## 12. Supplied visual references

- `mockups/storefront-home-desktop.svg/png`
- `mockups/storefront-home-mobile.svg/png`
- `mockups/storefront-home-carousel-slide-02.svg/png`
- `mockups/storefront-collection-desktop.svg/png`
- `mockups/storefront-product-colour-selection.svg/png`
- `mockups/admin-dashboard.svg/png`
- `mockups/admin-homepage-carousel.svg/png`
- `mockups/admin-product-colour-images.svg/png`
- `mockups/admin-users.svg/png`

The user-supplied direction is preserved under `mockups/reference/`. Original generated visual assets used by these mockups are under `mockups/assets/`; they are concept assets and require business approval before public use.

Implementation must match the hierarchy, density, palette and interaction intent—not blindly reproduce placeholder content or pixel coordinates.

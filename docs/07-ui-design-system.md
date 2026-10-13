# UI and Design System

## 1. Visual direction

Create a polished productivity interface inspired by modern document tools, without copying Google Drive's exact branding. Favor a calm, professional, readable design over decorative effects.

## 2. Before building

- Inspect the current Next.js structure.
- Reuse the existing CSS framework, component library, icons, and font setup when suitable.
- Avoid adding another UI framework if the project already has one.
- Keep design tokens centralized.

## 3. Design tokens

Define consistent tokens for:
- Primary and secondary colors.
- Page background and surface colors.
- Borders and separators.
- Success, warning, and error states.
- Typography family, sizes, weights, and line heights.
- Spacing scale.
- Border radii and shadows.
- Focus ring.
- Responsive breakpoints.

Choose colors after inspecting the existing brand/theme. Maintain adequate contrast.

## 4. Typography

- Use a readable font already available in the project when possible.
- Use a small, consistent weight scale (for example, regular, medium, semibold).
- Establish hierarchy for page title, section title, body, helper text, and metadata.
- Avoid tiny metadata text and inconsistent font weights.
- Avoid loading multiple font families without a clear reason.

## 5. Core screens

### Sign-in
- Clear product identity and explanation.
- Primary “Continue with Google” action.
- Loading and error feedback.
- Accessible button label and keyboard focus.

### Document workspace
- Navigation/sidebar where appropriate.
- Search and upload actions.
- Breadcrumbs for nested folders.
- File/folder list or grid with name, type, size, and modified date where relevant.
- Context actions for rename, download, and delete.
- Responsive behavior for smaller screens.

### Dialogs and feedback
- Rename dialog with validation.
- Delete confirmation with clear consequences.
- Upload progress/status where supported.
- Toast or inline success/error feedback.
- Empty, loading, no-results, and retry states.

## 6. Interaction rules

- Every visible control must work or be clearly disabled.
- Prevent duplicate form submissions.
- Show errors close to the relevant action.
- Do not display success before the backend confirms success.
- Use optimistic updates only if failures can be rolled back correctly.
- Keep animations subtle and respect reduced-motion preferences.

## 7. Accessibility and responsiveness

- Use semantic HTML.
- Provide accessible labels for icon-only buttons.
- Ensure visible keyboard focus.
- Support expected keyboard behavior in menus and dialogs.
- Maintain adequate contrast.
- Test at desktop, tablet, and mobile widths.
- Do not rely on color alone to communicate status.

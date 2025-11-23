# Chebyshev Filter Calculator - Design Guidelines

## Design Approach
**Selected Framework:** Material Design System
**Rationale:** This engineering calculation tool requires clarity, robust data presentation, and functional efficiency. Material Design provides excellent patterns for forms, tables, and data-dense interfaces while maintaining modern aesthetics.

**Core Principles:**
- Information clarity over decoration
- Efficient workflow for engineers
- Scannable data presentation
- Progressive disclosure of complexity

## Typography System

**Font Family:** Inter (primary), JetBrains Mono (numerical data)
- Headings: Inter, weight 600-700
- Body text: Inter, weight 400
- Numerical data: JetBrains Mono, weight 400 (monospaced for alignment)
- Labels/captions: Inter, weight 500

**Scale:**
- H1 (App title): 2rem
- H2 (Section headers): 1.5rem
- H3 (Card titles): 1.25rem
- Body: 1rem
- Data tables: 0.875rem
- Captions/labels: 0.75rem

## Layout System

**Container Structure:**
- Maximum width: 1200px for main content
- Side padding: 6 units on mobile, 8 units on desktop
- Vertical spacing rhythm: 4, 6, 8, 12, 16 units

**Grid System:**
- Desktop: Two-column layout (input panel 40% | results panel 60%)
- Tablet: Single column, stacked
- Mobile: Full-width, stacked

## Component Library

### Input Panel
**Card-based container with:**
- Rounded corners (radius: 2 units)
- Elevated appearance (shadow depth: medium)
- Internal padding: 6 units
- Section spacing: 6 units between form groups

**Form Elements:**
- Text inputs: Full-width, height 12 units
- Labels: Above input, weight 500, small spacing below (1 unit)
- Helper text: Below input, caption size
- Radio buttons for mode selection (single/batch)
- Input validation: Real-time with inline error messages
- Number steppers for filter order with +/- buttons

**Primary Action Button:**
- Height: 12 units
- Full-width on mobile, auto-width on desktop
- Position: Bottom of input card
- Label: "Calculate G-Values"

### Results Display

**Single Order Mode:**
- Large card with table presentation
- Header row: Filter parameters (order, ripple dB)
- Horizontal scrollable table on mobile
- Column headers: g0, g1, g2, ... gn, g(n+1)
- Data row: Numerical values with 5 decimal precision
- Visual differentiation: Alternating subtle backgrounds for odd/even columns
- Below table: Legend explaining element types (series inductors vs shunt capacitors)

**Batch Mode (Orders 1-30):**
- Compact table with fixed headers
- Sticky header row during scroll
- First column: Order number (bold)
- Remaining columns: g-values
- Zebra striping for row readability
- Virtual scrolling for performance (if needed)

**Table Typography:**
- Headers: Weight 600, uppercase, letter-spacing
- Data cells: Monospaced font for alignment
- Cell padding: 3 units vertical, 4 units horizontal

### Educational Elements

**Tooltip System:**
- Icon-triggered tooltips next to technical terms
- Small info icon (16x16px)
- Tooltip appearance: Elevated card with 4 units padding
- Max-width: 280px
- Position: Dynamic based on screen space

**Notes Section:**
- Collapsible accordion at bottom of results
- Contains technical explanations
- List format with bullet points
- Slightly recessed appearance

### Export Functionality
- Secondary button: "Export to CSV"
- Position: Top-right of results card
- Icon + text label
- Downloads formatted CSV file

## Spacing & Rhythm

**Consistent Units:**
- Primary spacing: 4, 6, 8 (most common)
- Large sections: 12, 16
- Micro-spacing: 1, 2

**Component Spacing:**
- Between cards: 8 units
- Card internal padding: 6 units
- Form field spacing: 4 units
- Table cell padding: 3 units vertical, 4 units horizontal

## Responsive Behavior

**Breakpoints:**
- Mobile: < 768px (single column)
- Tablet: 768px - 1024px (transitional)
- Desktop: > 1024px (two-column)

**Mobile Adaptations:**
- Stack input and results vertically
- Full-width cards
- Horizontal scroll for wide tables
- Collapsed tooltips expand on tap
- Sticky calculate button at bottom

## Data Presentation Best Practices

**Numerical Precision:**
- Consistent decimal places (5 for g-values)
- Monospaced alignment
- Scientific notation for very small/large values

**Visual Hierarchy in Tables:**
- Bold row/column headers
- Subtle borders between cells (1px)
- Adequate cell padding for touch targets
- Clear visual separation between header and data

## Accessibility

**Form Accessibility:**
- All inputs with proper labels (not just placeholders)
- ARIA labels for screen readers
- Keyboard navigation throughout
- Focus indicators on all interactive elements
- Error messages linked to inputs

**Table Accessibility:**
- Table headers with scope attributes
- Row/column headers properly marked
- Caption describing table content
- Keyboard navigable cells for batch mode

## Page Structure

**Header:**
- App title: "Chebyshev Filter Calculator"
- Subtitle: "Precision G-Values Calculation"
- Minimal, clean header with adequate vertical padding (6 units)

**Main Content Area:**
- Two-column layout (desktop)
- Left: Input panel (sticky on scroll)
- Right: Results panel (scrollable)

**Footer:**
- Technical notes section (collapsible)
- Reference formula information
- Minimal height, unobtrusive

## Animations
- Form validation: Subtle shake on error
- Results appearance: Fade-in when calculated
- Tooltip: Gentle scale-in (200ms)
- Mode switching: Crossfade transition (300ms)
- Avoid distracting motion during calculation
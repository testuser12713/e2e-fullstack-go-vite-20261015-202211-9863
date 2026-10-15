# Design — Project Identity

> This document is project-long-lived. Tokens are not changed without
> the Architect's approval. Developers MUST use these tokens
> instead of improvising their own colors/spacings.

## Style Direction

Calm, warm 'paper' light theme with a deep teal ink accent and amber stars — a tidy bookshelf feel with Linear/Stripe-level clarity and restraint.

## Colors

- `--color-bg`: **#FAF8F4**
- `--color-surface`: **#FFFFFF**
- `--color-surface_muted`: **#F3F0EA**
- `--color-fg`: **#1F2328**
- `--color-muted`: **#6B6F76**
- `--color-border`: **#E4DFD6**
- `--color-border_strong`: **#CFC8BC**
- `--color-accent`: **#0F6E6E**
- `--color-accent_hover`: **#0C5A5A**
- `--color-accent_soft`: **#E3F1F0**
- `--color-star`: **#E0A21B**
- `--color-star_empty`: **#D6D0C4**
- `--color-danger`: **#B42318**
- `--color-danger_soft`: **#FDECEA**
- `--color-success`: **#2F7D4F**
- `--color-focus_ring`: **#0F6E6E66**
- `--color-status_planned_bg`: **#EEF0F3**
- `--color-status_planned_fg`: **#4A5260**
- `--color-status_reading_bg`: **#FFF4DD**
- `--color-status_reading_fg`: **#8A5A00**
- `--color-status_read_bg`: **#E3F1EA**
- `--color-status_read_fg`: **#1F6B44**

## Typography

- `font_family`: Inter, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif
- `heading_font_family`: 'Source Serif 4', 'Source Serif Pro', Georgia, 'Times New Roman', serif
- `heading_weight`: 600
- `body_weight`: 400
- `label_weight`: 500
- `size_xs`: 12px
- `size_sm`: 14px
- `size_base`: 16px
- `size_lg`: 18px
- `size_xl`: 24px
- `size_2xl`: 32px
- `line_height_body`: 1.5
- `line_height_heading`: 1.25
- `numeric`: font-variant-numeric: tabular-nums for all counts and averages

## Spacing Scale

- `--space-0`: 4px
- `--space-1`: 8px
- `--space-2`: 12px
- `--space-3`: 16px
- `--space-4`: 24px
- `--space-5`: 32px
- `--space-6`: 48px

## Border-Radii

- `--radius-sm`: 4px
- `--radius-md`: 8px
- `--radius-lg`: 12px
- `--radius-pill`: 999px

## Components

### Button

Variants primary/secondary/ghost/danger. min-height 44px, padding 10px 16px, radius md, font 14px weight 500, gap 8px for icon+label. Primary: bg=accent, fg=#FFFFFF; hover bg=accent_hover; active translateY(1px) + bg=accent_hover; focus-visible 3px outline focus_ring offset 2px; disabled opacity 0.5, cursor not-allowed, no hover change, aria-disabled set. Secondary: bg=surface, 1px border border_strong, fg=fg; hover bg=surface_muted. Ghost: transparent, fg=muted; hover bg=surface_muted fg=fg. Danger: fg=danger transparent; hover bg=danger_soft. Loading state: label replaced by 'Speichern…' and disabled. Icon-only buttons are 44x44px with aria-label (e.g. 'Buch löschen').

### Input

Text field: height 44px, padding 0 12px, radius md, bg=surface, 1px border=border, fg=fg, placeholder=muted. Hover border=border_strong; focus border=accent + 3px ring focus_ring; error border=danger with helper text below in 13px danger (e.g. 'Bitte gib einen Titel ein.' / 'Bitte gib einen Autor ein.'), shown only after a submit attempt; disabled bg=surface_muted opacity 0.6. Label above field, 14px weight 500, 4px gap. Search variant has a leading magnifier icon (16px, muted), placeholder 'Titel oder Autor suchen…', clear 'x' ghost button with aria-label 'Suche leeren' when non-empty.

### AddBookForm

Card (surface, 1px border, radius lg, padding 24px). Heading 'Buch hinzufügen' (serif 18px). Desktop: Titel and Autor inputs side by side (flex 1 each) + primary button 'Hinzufügen' aligned to the input bottom, gap 12px. Mobile <640px: stacked, button full-width. Max length 200 enforced via maxLength. On API error show inline ErrorBanner inside the card. After success inputs clear and focus returns to Titel.

### FilterBar

Row above the list: segmented status control 'Alle' | 'Geplant' | 'Lese gerade' | 'Gelesen' (role=radiogroup or tablist) + search Input. Segmented: container bg=surface_muted radius md padding 4px; each segment min-height 36px (container 44px), padding 0 12px, 14px weight 500, fg=muted; selected segment bg=surface, fg=fg, subtle shadow 0 1px 2px rgba(0,0,0,0.06); arrow-key navigation. Desktop: segmented left, search right (max-width 320px). Mobile: stacked, segmented scrolls horizontally if needed, search full width. Show result count in muted 13px, e.g. '3 Bücher'.

### BookItem

List row/card: bg=surface, 1px border=border, radius lg, padding 16px, gap 12px between items. Top line: title (serif 18px weight 600, fg, wraps, word-break) and below author (14px muted, prefixed by nothing). Right/top-right: delete icon button (ghost→danger on hover, aria-label 'Buch „<Titel>“ löschen'); click shows inline confirm row 'Wirklich löschen?' with danger button 'Löschen' and ghost 'Abbrechen'. Bottom line: StatusSelect + StarRating, wrapping on mobile. When marked 'Gelesen' show '<muted 13px> Gelesen am 12.03.2025'. While a PATCH is in flight the affected control shows reduced opacity 0.6 and is disabled; on failure revert and show small danger text 'Änderung konnte nicht gespeichert werden.'. Newly added item gets a 600ms accent_soft background fade.

### StatusSelect

Native <select> styled as pill badge (keyboard + mobile friendly), aria-label 'Status'. Height 44px on touch, 36px visual pill inside, radius pill, padding 0 32px 0 12px, 14px weight 500, chevron icon right. Colors by value: 'Geplant' status_planned_bg/fg, 'Lese gerade' status_reading_bg/fg, 'Gelesen' status_read_bg/fg. Focus ring focus_ring. Disabled opacity 0.5.

### StarRating

role=radiogroup aria-label 'Bewertung'; 5 star buttons each role=radio with aria-label '1 Stern' … '5 Sterne', 44x44px hit area with 20px star icon. Filled=star, empty=star_empty. Hover previews fill up to hovered star; arrow keys change value, focus-visible ring. Clicking the currently selected star OR the trailing ghost button 'Bewertung entfernen' (only visible when a rating is set, icon 'x' 16px, 44px hit area) clears to null. Unrated shows muted 13px text 'Nicht bewertet' next to empty stars for screen readers via aria too.

### StatsPanel

Card (surface, 1px border, radius lg, padding 24px). Heading 'Statistik <Jahr>' e.g. 'Statistik 2025' (serif 18px). Two KPI tiles side by side (bg surface_muted, radius md, padding 16px): 'Gelesen in diesem Jahr' value 32px weight 600 tabular-nums; 'Ø Bewertung' value e.g. '4,2 ★' or '–' when null. Below: monthly bar chart, 12 columns 'Jan Feb Mär Apr Mai Jun Jul Aug Sep Okt Nov Dez' (12px muted labels), bars bg=accent radius sm top, max height 96px scaled to max month (min 2px for 0 as border color), count above bar 12px tabular-nums only if >0; each bar has aria-label e.g. 'März: 2 Bücher'. Refetches after every create/patch/delete; while refreshing keep old values with opacity 0.6. Desktop: sticky sidebar; mobile: placed above the list.

### EmptyState

Centered within list area, padding 48px 24px, dashed 1px border=border_strong, radius lg, bg transparent. Book icon 32px muted, title 16px weight 600, text 14px muted. Texts: no books at all → 'Noch keine Bücher' / 'Füge oben dein erstes Buch hinzu.'; filter/search no match → 'Keine Treffer' / 'Kein Buch passt zu Filter und Suche.' with secondary Button 'Filter zurücksetzen'.

### LoadingState

3 skeleton BookItem cards (surface_muted blocks, radius sm, pulse animation 1.2s, reduced-motion: static) plus visually hidden text 'Bücher werden geladen…' with aria-live=polite. Stats panel shows skeleton KPIs.

### ErrorBanner

bg=danger_soft, 1px border danger at 30% opacity, fg=danger, radius md, padding 12px 16px, 14px, leading alert icon, role=alert. API unreachable: 'Der Server ist nicht erreichbar. Bitte versuche es später erneut.' with secondary Button 'Erneut versuchen'. Server validation errors show the message from {error} prefixed by nothing; generic fallback 'Etwas ist schiefgelaufen.'

### AppHeader

Height 64px, bottom border=border, bg=bg. Left: wordmark 'Leseliste' serif 22px weight 600 fg with small book icon in accent. No nav needed.

## Layout Principles

- Container max-width 1080px, centered, horizontal padding 24px desktop / 16px mobile; page top padding 32px.
- Breakpoints: mobile <640px, tablet 640–959px, desktop ≥960px.
- Desktop ≥960px: CSS grid 'minmax(0,1fr) 320px', gap 32px — left column: AddBookForm, FilterBar, book list; right column: StatsPanel (position sticky, top 24px). Below 960px: single column in order AddBookForm, StatsPanel, FilterBar, list.
- Vertical rhythm: 24px between sections, 12px between list items, 16px inside cards between groups.
- All touch targets ≥44x44px; every interactive element has a visible focus-visible ring (focus_ring) and an accessible German label.
- Dates: German format DD.MM.YYYY (e.g. '12.03.2025') via Intl.DateTimeFormat('de-DE', {day:'2-digit', month:'2-digit', year:'numeric'}), always in local time; no times are shown.
- Average rating: one decimal with German comma via Intl.NumberFormat('de-DE', {minimumFractionDigits:1, maximumFractionDigits:1}) followed by ' ★' (e.g. '4,2 ★'); null shows '–'.
- Counts: integer tabular-nums with German pluralization — '1 Buch' / 'n Bücher' (0 → '0 Bücher').
- Month labels: fixed German short names 'Jan','Feb','Mär','Apr','Mai','Jun','Jul','Aug','Sep','Okt','Nov','Dez'; year as 4 digits.
- Status labels are always exactly 'Geplant', 'Lese gerade', 'Gelesen' (filter adds 'Alle'); map from API values planned/reading/read in one shared helper.
- All UI text German; every async action shows a pending state (disabled + opacity) so no control silently does nothing; respect prefers-reduced-motion.

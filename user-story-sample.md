# User Story 01: Advanced Review Search and Filtering

## User Story
As a VendorAdvisor user I want to search and filter vendor reviews using multiple criteria so that I can quickly find relevant reviews from specific teams, disciplines, vendors, and rating ranges to help make informed vendor selection decisions.

## Requirements
- Free text search across review titles and text content (case-insensitive)
- Filter by Team (dropdown selection)
- Filter by Discipline (dropdown selection)
- Filter by Vendor (searchable combo box with autocomplete)
- Filter by Minimum Rating (1-5 stars)
- Filter by Maximum Rating (1-5 stars)
- Display search results with review count
- Show reviews ordered by most recent first
- Preserve filter values in the search results page for refinement

## Implementation Plan

### 🎯 Requirements Analysis
**User Need**: Find specific vendor reviews quickly using multiple filter criteria to support procurement decisions

**Key Features Required**:
1. **Free Text Search**: Search across review title and text content
2. **Team Filter**: Select specific team that wrote the review
3. **Discipline Filter**: Filter by service category (e.g., Software Development, Design)
4. **Vendor Filter**: Searchable combo box for vendor selection
5. **Rating Range**: Min/Max rating filters for quality filtering
6. **Results Display**: Show filtered results with count and refinement options

### 📊 Database Structure Analysis
✅ **Review Model**: Contains all necessary fields (title, text, rating, team_id, discipline_id, vendor_id)
✅ **Relationships**: Review → Team, Review → Discipline, Review → Vendor (foreign keys)
✅ **Timestamp**: created_at field for ordering results
✅ **SQLAlchemy Support**: Flask-SQLAlchemy ORM for query building

### 🏗️ Technical Implementation Plan

#### Phase 1: Backend Search Endpoint (High Priority)
1. **Search Route** ([app.py:285-336](app.py#L285-L336)):
   - Route: `/search` with GET method
   - Query parameters: `team`, `discipline`, `vendor`, `rating` (min), `max_rating`, `search_text`
   - Sequential query building with SQLAlchemy filters
   - Case-insensitive ILIKE search for text fields
   - Order results by `created_at DESC`

2. **Filter Logic**:
   - Team filter: `Review.team_id == int(team_id)`
   - Discipline filter: `Review.discipline_id == int(discipline_id)`
   - Vendor filter: `Review.vendor_id == vendor_id` (string ID)
   - Min rating: `Review.rating >= int(min_rating)`
   - Max rating: `Review.rating <= int(max_rating)`
   - Text search: `db.or_(Review.title.ilike(pattern), Review.text.ilike(pattern))`

#### Phase 2: Frontend Search Interface (High Priority)
3. **Home Page Search Form** ([templates/index.html:12-93](templates/index.html#L12-L93)):
   - Free text input field for search query
   - Team dropdown (all teams from database)
   - Discipline dropdown (all disciplines from database)
   - Vendor combo box (searchable, all vendors from database)
   - Min rating dropdown (1-5 stars)
   - Max rating dropdown (1-5 stars)
   - Search button with Material Design icon

4. **Search Results Page** ([templates/search_results.html](templates/search_results.html)):
   - Same filter form with pre-selected values
   - Results count display
   - Review list with star ratings
   - Review metadata (vendor, team, discipline)
   - Truncated review text (200 chars)
   - "View Details" link for each review
   - Empty state message when no results

#### Phase 3: Enhanced User Experience (Medium Priority)
5. **Searchable Vendor Combo Box** ([static/combo-box.js](static/combo-box.js)):
   - Custom JavaScript component wrapping select element
   - Text input with autocomplete functionality
   - Dropdown list filtered by user input
   - Keyboard navigation support
   - Click-outside to close dropdown
   - Integrates with existing vendor select elements

6. **Material Design Styling** ([static/combo-box.css](static/combo-box.css)):
   - Consistent look with Material Design 3
   - Styled dropdown with hover states
   - Responsive layout for filter forms
   - Star rating visual display
   - Form row layout for multiple filters

### 🎨 User Interface Design
```
┌─────────────────────────────────────────────────────────┐
│ Find Reviews                                            │
├─────────────────────────────────────────────────────────┤
│ [Search in title and review text...              ] 🔍  │
│                                                         │
│ [Team ▼] [Discipline ▼] [Vendor 🔍] [Min ★ ▼] [Max ★▼]│
│                                                         │
│ [Search]                                                │
├─────────────────────────────────────────────────────────┤
│ Found 3 reviews                                         │
├─────────────────────────────────────────────────────────┤
│ Excellent Service ★★★★★                                │
│ Acme Corp • Engineering Team • Software Development    │
│ "Lorem ipsum dolor sit amet, consectetur..."           │
│ 2025-01-15                              [View Details] │
├─────────────────────────────────────────────────────────┤
│ Good Experience ★★★★☆                                  │
│ TechVendor • Design Team • UX/UI Design                │
│ "Sed do eiusmod tempor incididunt..."                  │
│ 2025-01-10                              [View Details] │
└─────────────────────────────────────────────────────────┘
```

### 🔍 Key Technical Challenges
1. **SQLAlchemy Query Building**: Sequential filter application with conditional logic
2. **Case-Insensitive Search**: ILIKE operator for PostgreSQL/SQLite compatibility
3. **Vendor String IDs**: Handle vendor_id as VARCHAR(5) not integer
4. **Filter State Preservation**: Pass filters dict to template for form pre-population
5. **Combo Box Integration**: Transform standard select into searchable component via JavaScript

### 📈 Success Metrics
- ✅ Users can search reviews by free text
- ✅ All filter combinations work correctly
- ✅ Vendor combo box provides searchable autocomplete
- ✅ Results display count and can be refined
- ✅ Filter values preserved after search
- ✅ Empty state handled gracefully
- ✅ Reviews ordered by most recent first
- ✅ Material Design consistent styling

## Implementation Status
🟢 **Completed** - Full search and filter functionality implemented with:
- Backend search endpoint with multi-criteria filtering
- Home page search form with all filter options
- Search results page with refinement capability
- Custom searchable vendor combo box component
- Material Design 3 styling throughout

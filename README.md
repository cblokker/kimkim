# Itinerary Highlights (V2) Technical Spec

### Objective

To create a V2 of the [itinerary highlights (V1)](https://github.com/kimkimtravel/interviews/blob/main/itinerary_highlights_v2.md) feature that will have the following use cases;


1.  As an `admin-user`, I want to be able to **CRUD** predefined highlights to any given `Hotel`, `Itinerary`, or `Activity` (with potential extendability to other objects in the future).
2. As an `admin-user`, I want to be able to select from a list of predefined highlights (created above) for any given `Hotel`, `Itinerary`, or `Activity`, and 
3. As a `travel-user`, I want to be able to view given highlights that my admin-user has selected/created on the activities. Render only if there are 3-5 highlights for a given `TravelPlan`, inclusively.
4. (Nice to have) For the 


## Implementation
### API
For this spec, the following will not be considered (but we can discuss);
- API versions (URL vs request header vs content type)
- Authentication (gem `devise`)
- Authorization of resources for given user types (gems `cancancan`, `pundit`)


1. **CRUD** for `PredefinedHighlight`, responsible for creating custom highligths for a given `Hotel`, `Activity`, or `Location`.
- 
  ```
  POST {base_url}/predefined_highlights
  ```
 

  
-
   ```
   GET {base_url}/predefined_highlights
   ```
   `query params`
   - type
   - id
   
- 
   ```
   PUT {base_url}/predefined_highlights
   ```
   
   `uri params`

-
   ```
   DELETE {base_url}/predefined_highlights
   ```


2. Showing predefined highlight(s) for a given trip plans

-
  ```
  GET {base_url}/trip_plan/:trip_plan_id/predefined_highlights
  ```
  
-
  ```
  GET {base_url}/trip_plan/:id/predefined_highlight/:id
  ```

  ```
  {
    id: int
    highlight_text: string,
    type: string (maps to enum in model + db)
  }
  ```


### Controllers

```ruby
def PredefinedHighlightsController < ApplicationController
  # TODO: CRUD scaffolding for custom highlights, to generate the polymorphic association
end
```

```ruby
def TripPlans::PredefinedHighlights < ApplicationController
  # TODO: intex & show for predefined highlights for a given trip plan
  def index
  end
  
  def show
  end
end
```



### Models

Questions:

1. Create a model `PredefinedHighlight` that will map with controller & db, `rails g model CustomHighlight`

```ruby
class CustomHighlight < ActiveRecord::Base
  validates_presence_of :highlight_text, :type
  belongs_to :custom_highlightable, polymorphic: true
  belongs_to :trip_plan
  attribute :highlight_text, :string
  attribute :type, :enum
...
end
```

```ruby
class Hotel < ActiveRecord::Base
  has_many :predefined_highlights
...
end
```

```ruby
class Activity < ActiveRecord::Base
  has_many :predefined_highlights
...
end
```

```ruby
class Location < ActiveRecord::Base
  has_many :predefined_highlights
...
end
```

```ruby
class TripPlan::Highlight < ActiveRecord::Base
  belongs_to :trip_plan
  belongs_to :photo
  attribute :highlight_text, :string
  attribute :position, :integer # random note: we can explore using a lexical sort to limit writes to db - less locking.
...
end
```




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


1. CRUD for Highlights
 
Description: Responsible for creating custom highligths for a given `Hotel`, `Activity`, or `Location`.
```
POST {base_url}/custom_highlights
```
`uri params`
- type
- id 

Description: Responsible for editing custom highligths for a given `Hotel`, `Activity`, or `Location`.
```
PUT {base_url}/custom_highlights
```
`uri params`

Description: Responsible for deleting custom highligths for a given `Hotel`, `Activity`, or `Location`.
```
DELETE {base_url}/custom_highlights
```
`uri params`

Description: Show custom hightligts for a given 
```
GET {base_url}/trip_plan/:id/custom_highlights
```

```json
{
  id: int
  highlight_text: string,
  type: string
},{}
```




Assigning a custom highlight to


An endpoint for exposing 3 highlights, the of which match a user profile's likeability concept, and a hilight type


### Controllers

```ruby
def CustomHighlightController

  # 
  def create
  end
  
  #
  def edit
  end
end
```



### Models

Questions:
1. Do we need to preserve 

1. Create a model `CustomHighlight` that will map with controller & db, `rails g model CustomHighlight`

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
class TripPlan::Highlight < ActiveRecord::Base
  belongs_to :trip_plan
  belongs_to :photo
  attribute :highlight_text, :string
  attribute :position, :integer # random note: we can explore using a lexical sort to limit writes to db - less locking.
...
end
```


### Database & migrations






### Service Objects

1. On creating a custom 

```ruby
class UseCase::CreateTripPlanHighLight
  def initialize()
  end
  
  def call
    
  end
  
  private
  
end
```

### Deployment/Launch Checklist
[ ]







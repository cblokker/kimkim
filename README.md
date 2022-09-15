# kimkim

## API
For now, we won't consider API versions. We will add endpoints any assumed current API version

Custom Highlights
Description: Responsible for creating custom highligths for a given `Hotel`, `Activity`, or `Location`.
`POST {base_url}/custom_highlights`
`uri params`

Description: Responsible for editing custom highligths for a given `Hotel`, `Activity`, or `Location`.
`PUT {base_url}/custom_highlights`
`uri params`

Description: Responsible for deleting custom highligths for a given `Hotel`, `Activity`, or `Location`.
`DELETE {base_url}/custom_highlights`
`uri params`


Assigning a custom highlight to


An endpoint for exposing 3 highlights, the of which match a user profile's likeability concept, and a hilight type


## Controllers

```ruby
def 
end
```


## Models
```

```


## Database & migrations






## Service Objects

1. We will need a method, or service object, to clone a preset







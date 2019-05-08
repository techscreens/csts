# Developer Comments

## Approaches

* In my existing production app I have an additional postcss plugin
  installed for nesting css (this is not available using Create React App).
  I personally prefer the nested CSS approach as I believe it leads
  to more readable code.
  
* As local storage is a synchronous operation I have wrapped the persistence
  to storage in a debounce as a way to help ensure the app remains responsive
  while the user updates. An alternative approach would be to write localstorage
  updates in an idle callback.
  
* I have used the selector pattern to ensure any future refactoring of the
  store state should only require refactoring of the selectors and not any
  other areas of the app
  
* I have not used PropTypes as I prefer to use flow or typescript with a babel
  plugin to generate the PropTypes - this has the advantage of providing both
  compile time and dev runtime type checking. I see in the Tech Radar that
  typescript would appear to be your preferred approach for this

## Testing

* I have used hooks as a way of using a reducer pattern
  without having to install redux (which would be overkill for
  this project)

* Whilst the README states you currently use enzyme for testing
  I have used react testing library in this project as enzyme
  does not yet support hooks.
  
* Due to time constraints I have only fully implemented tests for
  Tile, Icons and reducer. I have added test files and todos in the
  locations I would write additional unit tests.
  
* Ideally additional integration tests using a tool such as cypress
  would provide additional coverage in a real browser environment

## Enhancements
* Currently the idea ordering is performed in real-time. This causes
  a jump in the card position if the start of the title is changed
  while sorted by title. This could be mitigated by caching the sort
  order and dispatching a resort action on blur

* I did not add an unobtrusive notification for updates in the time.
  There are two possible approaches for this - either using the browser
  Notification API or an on screen "feedback stack". I have previously
  implemented a feedback stack using redux-middleware which combined with
  redux-promise allows automatic dispatching of actions to add items
  to the feedback stack when a fulfilled or rejected action is fired.
  This is achieved by executing onSuccessFeedback or onErrorFeedback
  functions if defined in the action meta.
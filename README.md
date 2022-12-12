# Re-Cart
Simple cart page using useContext api in react 🛒

This is a [React.js](https://reactjs.org/) project 
​
## Git branching model
​
### Branches
​
There are 3 main branches:
​
- `develop` - The development branch. It contains the latest state of the project. This is the main branch for the
  developers.
​
  All the new features has to be merged to the development environment and tested properly before they can go live.
​
- `staging` - The pre-production testing branch. All the updates that was properly tested on the
  development environment and ready to the production should be tested first on the isolated
  production environment - the staging environment.
​
  Often the development environment has specific tweaks on, making their development and testing experience
  more convenient. It's also may contain some unfinished and not properly tested flows. But on the production
  environment with different configuration and feature set the application may behave different. Here's why we need
  the staging environment.
​
- `main` - The production branch. Only the latest stable build can be merged to the `main` branch
​
For any new update must be created a separate branch from the `develop` branch. The branch name should written in
kebab-case and contain the id of a specific ticket on the task management environment like Jira/Trello/etc.
The every branch should be related to a specific ticket, but in rare cases it can be ignored.
​
Examples:
​
- `MD-1222`
- `MD-1222-gallery-navigation`
​
### Merging order
​
The merging order is strict: `feature` -> `develop` -> `staging` -> `main`. Nothing should be merged directly to the `main` past
the `staging` or `develop` branch same as nothing should be merged to the `staging` past the `develop` branch. All the
new update has to be done in a separate branch created from the `develop` branch. Later it can be merged to the `develop`
branch through merge(pull) request.
​
### Commit structure
​
The commit structure should look as follows:
​
`[type*]: [task_id] [short_description*]`
​
- `type` - The update type. It can be one of the following: `feat`(new feature/functionality), `refactor`, `fix`,
  `chore`(anything else)
- `task_id` (optional) - Id of a specific ticket on the task management environment like Jira/Trello/etc. The every commit/update
  should be related to a specific ticket (can be ignored in rare cases).
- `short_description` - The meaningful description of the updates made. The description like "Fix" or "Bug fix" is not sufficient.
  It should be more specific, like: "Gallery navigation fix"
​
Examples:
​
- `feat: MD-1222 Gallery navigation`
- `fix: MD-1222 Gallery navigation fix`
- `refactor: MD-1222 Refactor gallery navigation component`
- `chore: MD-1222 Remove unused imports`
​
### Merge(Pull) requests
​
#### Naming
​
The merge request name structure should look as follows:
​
`[task_id] [short_description*]`
​
- `task_id` (optional) - Id of a specific ticket on the task management environment like Jira/Trello/etc. The every commit/update
  should be related to a specific ticket (can be ignored in rare cases).
- `short_description` - The meaningful description of the updates made. The description like "Fix" or "Bug fix" is not sufficient.
  It should be more specific, like: "Gallery navigation fix"
​
Example: `MD-1222 Gallery navigation`
​
#### Label system
​
Each pending merge request has to be labeled with a certain status. **Only one label can be active at the same time**:
​
- `new` - The developer have to set this label when he creating a new MR. This will mark the branch as "ready to review"
- `review` - The reviewer sets this label while review is in progress. It's not recommended to update your MR while the
  review label is active. The reviewer has to finish the review round before the developer can proceed on any update
- `feedback` - The reviewer setting this label after he finishes the review round. When the developer sees this label on
  his MR, he has to collect feedback and apply updates if needed.
- `wip` - Work In Progress. The developer sets this status while his work on this branch is in progress. While this label
  is active the reviewer can not add any comments and has to wait until the status is set to `updated` by the developer.
  While developer is working on the updates he should not be distracted by the new comments
- `updated` - The developer sets this label when he finished updates on the current MR.
- `ready` - A reviewer who does not have permission to merge should set this status to the MR when it's ready to merge.
  The developer should set this status after the `feedback` stage, in case he read the review and is not going to make
  any updates. This can happen if the review is advisory in nature and does not require any updates. When the reviewer
  sees this label he knows that the developer have read the review, and didn't any updates, so the MR can be merged now.
- `merge-conflict` - Marking requests with merge conflicts for better visibility.
- `postponed` - Marking postponed MR
​
## Styling
​
- On this project the SASS(SCSS) syntax is used for styling.
- The global styles should be defined inside the base style directory
  (`/styles`).
- The local styling for the components should be defined using the modules (`[name].module.scss`) and located inside the component's directory
- Inline styling is not allowed for any common case. Exceptions are the cases when it's not possible to handle styling
  without the inline style definition, for example when you need to pass a prop or variable from the render function:
​
```jsx harmony
<div style={{width: '40px', height: '20px'}} /> // NOT ALLOWED!
// - Must use a stylesheet to set theese properties
​
<div style={{width: `${boxWidth}px`, height: `${boxHeight}px`}} /> // IS ALLOWED
```
​
### Themes
​
- Theme variables must be defined inside a `styles/_theme.scss`. Any theme variable can only be defined here.
- For the every color/background should be specified a unique theme variable. There are can be the common variables used
  in a several places, but it's recommended to create a unique variables for the every reusable
  component to make it more discrete or independent:
​
```css
/* The common variables. Can only be used to style the common cases */
--border-color: #eee;
--font-color: #000;
​
/* The variables specific to the Button component. 
   Can only be used inside the Button component style definition */
--button-border-color: #eee;
--button-font-color: #000;
```
​
#### Constant naming format:
​
`--[component]-[specific]-[property]?-[modifier]`
​
### Breakpoints
​
- Use breakpoint mixins located in `/styles/mixins/_breakpoints.scss` to define a breakpoint-specific styles. For the
  common cases use only the `breakpoint($breakpoint)` mixin with defined breakpoint variables: `sm-max`, `md-max`, `sm-min`,
  `md-min`, etc. For the very rare cases a custom media query can be used.
- Describe media queries inside a target class style definition block - do it SASS(SCSS) way:
​
```scss
// BAD:
​
.container {
  max-wdth: 1440px;
  //...
}
​
@include breakpoint(sm-max) {
  .container {
    max-width: 100%;
  }
}
​
// GOOD:
​
.container {
  max-wdth: 1440px;
  //...
​
  @include breakpoint(sm-max) {
    max-width: 100%;
  }
}
```

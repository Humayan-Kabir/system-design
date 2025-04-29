### Redux without toolkit
- for each feature part we need:
	1. action constants
	2. action creators
	3. thunk function which does async call then dispatch action 
	4. reducers
* finally we need to combine reducers to root-reducer
* in store we need to apply thunkMiddleware
### Redux with toolkit
* for each feature part it is repetitive to define action, action creator, write reducer where need to handle multiple actions
* with RTK we don't need to create action constants, action creators, we need to write just each action reducer code, rtk will create final reducer. name will be given by rtk query
* if you need to handle other actions, 
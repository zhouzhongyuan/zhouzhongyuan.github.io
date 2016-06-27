#React.js 错误记录
1.
```error
warning.js?8a56:45 Warning: Failed Context Types: Required context `muiTheme` was not specified in `List`. Check the render method of `FluxContainer(DictPicker)`.
```
```
ListItem.js?b121:399 Uncaught (in promise) TypeError: Cannot read property 'prepareStyles' of undefined(…)
```
中文解释: List的parent Component没有Theme,需要自己添加Theme
解决办法:
```javascript  
 import getMuiTheme from 'material-ui/styles/getMuiTheme';
 import MuiThemeProvider from 'material-ui/styles/MuiThemeProvider';
 
                <MuiThemeProvider muiTheme={getMuiTheme()}>
                    <List onTap={(event)=>this.onClick(event)} onValueChange={(v)=>this.onValueChange(v)} >
                        {
                            itemList
                        }
                    </List>
                </MuiThemeProvider>
```
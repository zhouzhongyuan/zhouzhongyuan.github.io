# ESLint入门
##原始教程

[ESLint官方教程](http://eslint.org/docs/user-guide/getting-started)

[eslint-config-airbnb](https://github.com/airbnb/javascript/tree/master/packages/eslint-config-airbnb)

##步骤
以airbnb的javascript规范为例。
### 1.npm init
新建文件夹,并进入
```bash
mkdir learn-eslint
cd learn-eslint
```
```bash
npm init
```
一直按确定[Enter]键
### 2.修改package.json
添加如下内容:
```json
  "eslintConfig": {
    "env": {
      "browser": true,
      "node": true
    }
  }
```
### 3.添加eslint相关依赖

```bash
npm install --save-dev eslint-config-airbnb eslint-plugin-import eslint-plugin-react eslint-plugin-jsx-a11y eslint
```
### 4.添加 .eslintrc 文件
新建文件 .eslintrc
可以使用如下命令新建文件,你也可以不用下述命令。只要learn-eslint文件夹下有这个文件就行。
```bash
touch .eslintrc
```

编辑 .eslintrc

```json
{
  "extends": "airbnb",
  "plugins": ["react"],
  "parser":"babel-eslint",
  "rules": {
    "strict": 0,
    "indent": ["error", 4],
  }
}
```
### 5.执行eslint
可以使用命令行执行(不讲了);

也可以使用gulp

gulpfile.js如下
```javascript
var gulp = require('gulp');
var eslint = require('gulp-eslint');
var gulpIf = require('gulp-if');

gulp.task('lint', function() {
    return gulp.src('DictList.js')
        .pipe(eslint())
        .pipe(eslint.format());
});

var gulpIf = require('gulp-if');
function isFixed(file) {
    return file.eslint && typeof file.eslint.output === 'string';
}
gulp.task('lint-fix', function() {
    return gulp.src('DictList.js')
        .pipe(eslint({ fix: true }))
        .pipe(eslint.format())
        .pipe(gulpIf(isFixed, gulp.dest('./dist')));
});
```
其中,DictList.js是你要检测的文件名称,要自行替换奥。

在learn-eslint文件夹下执行
```bash
gulp lint
```
就能看到你的检测结果了。

如果在使用过程中提示没有**,别忘了 npm install **。

##常见rules
```json
    "indent": ["error", 4],   //缩进
    
    "no-multiple-empty-lines": ["error", { "max": 0, "maxBOF": 0}], //检测有没有空行
    
    "linebreak-style": ["error", "unix"],
    
    "semi": ["error", "always"],
    
    "no-cond-assign": ["error", "always"],
    
    "no-console": "off",
    
    "jsx-quotes": ["error", "prefer-double"]
    
```

### 检测console.log
```eslint
    "no-console": ["error", { "allow": ["warn", "error"] }],
```
上述rule的意思是: 检测console行,只检测console.log,不检测console.warn和console.error

```javascript

    "react/jsx-indent":"off",
    "react/jsx-indent-props":"off"

```
由于我的eslint 是extend自airbnb,缩进(react/jsx-ident和react/jsx-indent-props)总是提示错误,但是我看了没有什么问题,所以就要覆盖掉原来的rules。上述代码就是关闭检测的意思。

##遇到的问题

[object-shorthand1](http://eslint.org/docs/rules/object-shorthand) [object-shorthand2](http://stackoverflow.com/questions/36093638/unexpected-block-statement-surrounding-arrow-body)

[no-multiple-empty-lines](http://eslint.org/docs/rules/no-multiple-empty-lines)
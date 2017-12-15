# gulp自动化工作流环境搭建
## 第一步：创建项目
### 初始化项目
- 命令行输入
```
npm init
```
- 安装gulp项目的依赖
```
npm install gulp --save-dev
npm install gulp-autoprefixer --save-dev
npm install gulp-concat --save-dev
npm install gulp-cssnano --save-dev
npm install gulp-imagemin --save-dev
npm install gulp-jshint --save-dev
npm install gulp-rename --save-dev
npm install gulp-sass --save-dev
npm install gulp-uglify --save-dev
npm install jshint --save-dev
npm install browser-sync --save-dev
npm install mkdirp --save-dev
```
> 安装完以后，package.json的文件为：
```
{
  "name": "gulp-workflow",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "browser-sync": "^2.18.13",
    "gulp": "^3.9.1",
    "gulp-autoprefixer": "^4.0.0",
    "gulp-concat": "^2.6.1",
    "gulp-cssnano": "^2.1.2",
    "gulp-imagemin": "^4.0.0",
    "gulp-jshint": "^2.0.4",
    "gulp-rename": "^1.2.2",
    "gulp-sass": "^3.1.0",
    "gulp-uglify": "^3.0.0",
    "jshint": "^2.9.5",
    "mkdirp": "^0.5.1"
  }
}

```
### 创建目录结构
> 创建一个src的文件作为源文件存放的位置。创建一个dist目录作为源文件打包后的位置，创建build文件放置一些gulp配置文件
```
- project
  |- build
  |- dist // 打包文件夹
  |- src  // 源文件夹
  | |- assets // 放置一些第三方文件，如bootstrap
  | |- css
  | |- images
  | |- js
  | |- sass
  |- gulpfile.js
  |- package.json
```
## 第二步：编写gulp配置
### 创建gulp的config文件
> 我们在bulid文件夹中可以创建一个gulpfile.config.js文件，主要用来存放项目的目录配置，如源文件存放的路径，打包后文件存放的路径，你可以根据您的需要灵活的配置这个文件。同时将Config对应暴露出来供其他文件引用。
```
<!-- gulpfile.config.js -->
var SRC_DIR = './src/';     // 源文件目录  
var DIST_DIR = './dist/';   // 文件处理后存放的目录  
var DIST_FILES = DIST_DIR + '**'; // 目标路径下的所有文件  

var Config = {
    src: SRC_DIR,
    dist: DIST_DIR,
    dist_files: DIST_FILES,
    html: {  
        src: SRC_DIR + '*.html',  
        dist: DIST_DIR  
    },  
    assets: {  
        src: SRC_DIR + 'assets/**/*',            // assets目录：./src/assets  
        dist: DIST_DIR + 'assets'                // assets文件build后存放的目录：./dist/assets  
    },  
    css: {  
        src: SRC_DIR + 'css/**/*.css',           // CSS目录：./src/css/  
        dist: DIST_DIR + 'css'                   // CSS文件build后存放的目录：./dist/css  
    },  
    sass: {  
        src: SRC_DIR + 'sass/**/*.scss',         // SASS目录：./src/sass/  
        dist: DIST_DIR + 'css'                   // SASS文件生成CSS后存放的目录：./dist/css  
    },  
    js: {  
        src: SRC_DIR + 'js/**/*.js',             // JS目录：./src/js/  
        dist: DIST_DIR + 'js',                   // JS文件build后存放的目录：./dist/js  
        build_name: 'build.js'                   // 合并后的js的文件名  
    },  
    img: {  
        src: SRC_DIR + 'images/**/*',            // images目录：./src/images/  
        dist: DIST_DIR + 'images'                // images文件build后存放的目录：./dist/images  
    }  
};

module.exports = Config;

```
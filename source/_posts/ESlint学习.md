---
title: ESlint学习
date: 2017-07-02 14:05:11
tags:
---

定义：

- 用于JavaScript和JSX 的可插拔的linting 实用程序

安装：

- 本地安装： npm install eslint --save-dev

- 本地设置配置文件：./node_modules/.bin/eslint --init

- 执行任何文件或者文件夹的检查：./node_modules/.bin/eslint yourfile.js

- 全局安装：npm install eslint -g

- 全局安装之后执行某个文件或者文件夹的检查的时候，如果需要依赖插件，那么插件也需要全局安装，否则使用局部安装

使用：

- "semi": ["error", "always"] 其中的第一个值是级别，可以是以下值：


    - "off"或0：关闭规则
    - "warn"或1：将规则作为警告（不影响退出代码）
    - "error"或2：将规则作为错误（退出代码将为1）
-  启用默认的检查规则，在配置中加入："extends": "eslint:recommended"


配置：

- 配置ESlint的主要途径：

    - 使用js注释的方式直接将配置嵌入到文件中；

    - 使用配置文件，配置文件会对整个文件夹及其子文件夹的所有文件生效；

    - 可以在package.json中增加eslintConfig字段来对eslint进行配置；

    - 直接使用命令行指定检查规则。

- 配置信息：
    - Environments：检查脚本要执行的环境，同时可以在里面指定这个环境执行时需要的预定义的常量配置；

    - Globals：脚本在执行的时候需要访问的其他全局变量；
    - Rules：检查规则

解析器选项：

- 解析器选项允许制定需要的js选项，默认情况下ESlint使用ES5语法，可以通过配置的方式来覆盖默认的配置，同时也可以添加jsx的支持；

- 注意：支持jsx语法与支持react不同，使用react建议增加eslint-plugin-react模块；
- parserOptions支持的配置选项：
    - ecmaVersion：可以设置为3, 5(默认), 6, 7, 8，也可以设置为2015,2016这样的年份值；
    - sourceType：默认为"script"，如果使用ES6的模块，就设置为"module"；
    - ecmaFeatures：一个设置js特性的配置对象，可以有以下属性：
        - globalReturn：允许在全局作用域下使用return；
        - impliedStrict：启用全局严格模式（如果是js版本是5或者更高才可以）；
        - jsx：启用jsx；
        - experimentalObjectRestSpread：启用对象的...操作符展开；

定制解析器：

- 默认情况下，ESLint使用Espree作为解析器，只要解析器满足以下要求，可以选择指定在配置文件中使用不同的解析器：

    - 必须是一个本地安装的npm模块；

    - 必须有一个有Espree导出的接口（parse()方法）；

    - 必须生成与Esprima兼容的AST和token对象。

- 即使有这些兼容性，也不能保证外部解析器能够与ESLint正常工作，ESLint不会修复与其他解析器不兼容的错误；

- 使用方式：

- 注意，使用自定义解析器时，parserOptionsESLint默认情况下仍然需要配置属性才能正常使用ECMAScript 5中的功能。解析器都被传递parserOptions，并可能使用或不使用它们来确定要启用的功能。

指定环境：

- 环境定义了预定义的全局变量。可用的环境是：
    - - browser - 浏览器全局变量。
    - - node - Node.js全局变量和Node.js范围。
    - - commonjs - CommonJS全局变量和CommonJS范围（将其用于仅使用Browserify / WebPack的浏览器代码）。
    - - shared-node-browser - Node和Browser共同的全局。
    - - es6- 启用除模块之外的所有ECMAScript 6功能（这将自动将ecmaVersion解析器选项设置为6）。
    - - worker - 网络工作者全局变量。
    - - amd- 根据amd规范定义require()和define()作为全局变量。
    - - mocha - 添加所有的摩卡测试全局变量。
    - - jasmine - 添加1.3和2.0版本的所有Jasmine测试全局变量。
    - - jest - Jest全局变量。
    - - phantomjs - PhantomJS全局变量。
    - - protractor - 量角器全局变量。
    - - qunit - QUnit全局变量。
    - - jquery - jQuery全局变量。
    - - prototypejs - Prototype.js全局变量。
    - - shelljs - ShellJS全局变量。
    - - meteor - 流星全球变量。
    - - mongo - MongoDB全局变量。
    - - applescript - AppleScript全局变量。
    - - nashorn - Java 8 Nashorn全局变量。
    - - serviceworker - 服务工作者全局变量。
    - - atomtest - 原子测试助手全局变量。
    - - embertest - Ember测试助手全局变量
    - - webextensions - WebExtensions全局变量
    - - greasemonkey - GreaseMonkey全局变量

- 这些环境不是相互排斥的，因此您可以一次定义多个；

- 可以在文件内部，配置文件中或使用--env 命令行标志指定环境

- 要指定配置文件中的环境，请使用该env键，并通过设置每个环境指定要启用的环境true。例如，以下功能可以启用浏览器和Node.js环境：

- 如果要使用插件的环境，请确保在plugins数组中指定插件名称，然后使用未修复的插件名称，后跟斜杠，后跟环境名称。例如：

指定全局变量：

- no-undef这个规则会提示当使用没有在当前文件定义的全局变量的使用，如果要在文件中使用全局变量，那最好给ESLint配置这些全局变量；

- 指定全局变量的方式：

    - 使用注释的方式指定全局变量：

    - 如果要指定这两个变量不可修改：

    - 要在配置文件中配置全局变量，请使用该globals键并指出要使用的全局变量。设置每个全局变量名称等于true允许变量被覆盖或false不允许覆盖。例如：

    - 启用no-global-assign规则以禁止对代码中的只读全局变量进行修改。

配置插件：

- ESLint支持使用第三方插件。在使用插件之前，您必须使用npm进行安装；

- 要在配置文件中配置插件，请使用plugins包含插件名称列表的键。该eslint-plugin-前缀可以从插件名称被省略：

- 全局安装的ESLint实例只能使用全局安装的ESLint插件。本地安装的ESLint可以使用本地和全球安装的ESLint插件。

配置规则：

- 要使用配置注释在文件内部配置规则，请使用以下格式的注释：

- 上面例子中，eqeqeq被关闭并curly作为错误被打开。您还可以使用等价于规则严重性的数值：

- 如果规则有其他选项，则可以使用数组文字语法来指定它们，例如：

- 要在配置文件中配置规则，请使用该rules键以及错误级别和要使用的任何选项。例如：

- 要配置在插件中定义的规则，您必须在规则ID的前面加上插件名称和a /。例如：

- 配置在插件中定义的规则，也可以使用注释：

- 注意：从插件中指定规则时，请确保省略eslint-plugin-。ESLint在内部仅使用非原始名称来定位规则。

使用行内注释禁用规则：

- 要临时禁用文件中的规则警告，请使用以下格式的块注释：

- 禁用或启用特定规则的警告：

- 要在整个文件中禁用规则警告，请在文件/* eslint-disable */的顶部放置一个块注释；

- 禁用或启用整个文件的特定规则：

- 要禁用特定行上的所有规则，请使用以下格式之一的行注释：

- 禁用特定行上的多个规则：

- 上述方法也适用于插件规则。例如，要禁用eslint-plugin-example的rule-name规则，结合插件的名称（example）和规则的名称（rule-name）为example/rule-name：

- 注意：对文件的一部分禁用警告的注释告诉ESLint不会报告禁用代码的规则违规。然而，ESLint仍然解析整个文件，所以禁用的代码仍然需要在语法上有效的JavaScript

添加共享设置：

- ESLint支持将共享设置添加到配置文件中。您可以将settings对象添加到ESLint配置文件，并将其提供给将要执行的每个规则。如果您添加自定义规则并希望他们能够访问相同的信息并且易于配置，这可能很有用:

指定配置文件进行检查：

- 将文件保存在任何地方，并使用该-c选项将其位置传递给CLI

- 配置文件中的设置将覆盖默认设置

配置文件格式：

- ESLint支持多种格式的配置文件：
    - - JavaScript - 使用.eslintrc.js和导出包含您的配置的对象。
    - - YAML - 使用.eslintrc.yaml或.eslintrc.yml定义配置结构。
    - - JSON - 用于.eslintrc.json定义配置结构。ESLint的JSON文件还允许使用JavaScript风格的注释。
    - - 已弃用 - .eslintrc可以是JSON或YAML。
    - - package.json - eslintConfig在package.json文件中创建一个属性，并在那里定义您的配置

- 如果同一目录中有多个配置文件，ESLint将只使用一个。优先顺序是：
    - - .eslintrc.js
    - - .eslintrc.yaml
    - - .eslintrc.yml
    - - .eslintrc.json
    - - .eslintrc
    - - package.json

配置级联和层次：

- 配置采用就近原则;

- 注意：如果您的主目录（~/.eslintrc）中有个人配置文件，则只有在找不到其他配置文件时才会使用。由于个人配置将适用于用户目录中的所有内容（包括第三方代码），因此运行ESLint时可能会导致问题。

- 默认情况下，ESLint将在根目录下的所有父文件夹中查找配置文件。如果您希望所有项目遵循一定的惯例，但有时会导致意想不到的结果，这将非常有用。要将ESLint限制在特定的项目中，请放置"root": true在文件的eslintConfig字段内package.json或.eslintrc.*文件中的项目根级别。一旦发现配置，ESLint将停止查找父文件夹"root": true。

- 从最高优先级到最低优先级的完整配置层次结构如下：

    - 内联配置：
        - /*eslint-disable*/ 和 /*eslint-enable*/
        - /*global*/
        - /*eslint*/
        - /*eslint-env*/

    - 命令行选项：
        - --global
        - --rule
        - --env
        - -c， --config

    - 项目级配置：
        - .eslintrc.*或package.json文件在与linted文件相同的目录中

        - 继续搜索.eslintrc和package.json祖先目录中的文件（父级具有最高优先级，然后是祖父母等），直到并包括根目录或直到找到配置"root": true。

        - 在（1）至（3）中没有任何配置的情况下，可以回到个人默认配置 ~/.eslintrc。

扩展配置文件：

- 配置文件可以从基本配置扩展启用的规则，使用extends属性，其值可以是：

    - 一个指定配置的字符串；

    - 一组字符串：每个配置会扩展前面声明的配置
- ESLint可以递归扩展配置，因此基本配置也可以具有extends属性，该rules属性可以执行以下任何操作来扩展（或覆盖）一组规则：

    - 启用其他规则；

    - 更改继承的规则的严重性，而不更改其选项：

        - 基本配置： "eqeqeq": ["error", "allow-null"]

        - 派生配置： "eqeqeq": "warn"

        - 实际配置： "eqeqeq": ["warn", "allow-null"]

    - 从基本配置覆盖规则的选项：

        - 基本配置： "quotes": ["error", "single", "avoid-escape"]

        - 派生配置： "quotes": ["error", "single"]

        - 实际配置： "quotes": ["error", "single"]

使用"eslint:recommended"：

- 使用这个配置会使用当前ESLint主版本中规定的所有推荐的规则，推荐的规则只在主版本中变动；

指定Lint的文件扩展名：

- 目前，告诉ESLint的唯一方法是使用--ext命令行选项指定一个逗号分隔的扩展列表。请注意，此标志仅与目录一起生效，如果与文件名或glob模式一起使用，将会被忽略。

忽略文件和目录：

- 您可以通过.eslintignore在项目的根目录中创建一个文件来告诉ESLint忽略特定的文件和目录。该.eslintignore文件是一个纯文本文件，其中每行是一个glob模式，指示哪些路径应从linting中省略。例如，以下将省略所有JavaScript文件：

- 当ESLint运行时，它会在当前工作目录中查找.eslintignore文件，然后再确定哪些文件为lint。如果找到此文件，则在遍历目录时会应用这些首选项。一次只能使用一个.eslintignore文件，因此.eslintignore不会使用当前工作目录中的文件。

- 使用node-ignore匹配Globs ，因此可以使用许多功能：

    - 开始的行#被视为注释，不影响忽略模式。

    - 路径是相对于.eslintignore位置或当前工作目录。这也影响要Lint的路径--ignore-pattern。

    - 忽略模式与.gitignore相同

    - 前面的行!是否定的模式，重新包含被早期模式忽略的模式。

- 除了在任何模式.eslintignore文件，ESLint总是忽略文件/node_modules/*和/bower_components/*

使用备份文件：

- 如果您希望使用.eslintignore与当前工作目录不同的文件，则可以使用该--ignore-path选项在命令行中指定它。例如，您可以使用.jshintignore文件，因为它具有相同的格式：

- 您也可以使用您的.gitignore文件

- 任何遵循标准忽略文件格式的文件都可以使用。请注意，指定--ignore-path意味着任何现有.eslintignore文件将不被使用。请注意，.eslintignore遵循.gitignore的规则。

忽略文件警告：

- 将目录传递给ESLint时，文件和目录将被忽略。如果您将特定文件传递给ESLint，则会看到一条警告，指示该文件已被跳过：

- 发生此消息是因为ESLint不确定是否要实际提示文件。如消息所示，您可以使用--no-ignore省略忽略规则。



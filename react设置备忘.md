使用Antd，无antd样式，还报错：
The “injectBabelPlugin” helper has been deprecated as of v2.0.
找寻问题解决方案中，要首先安装几个包：
确保你安装’customize-cra’并react-app-rewired@2.x
确保你安装’less’和’less-loader’

yarn add less less-loader

yarn add customize-cra

yarn add react-app-rewired@2.x

const {
    override,
    fixBabelImports,
    addLessLoader,
  } = require("customize-cra");

  module.exports = override(
    fixBabelImports("import", {
      libraryName: "antd", libraryDirectory: "es", style: true // change importing css to less
    }),
    addLessLoader({
      javascriptEnabled: true,
      modifyVars: { "@primary-color": "#1DA57A" }
    })
  );
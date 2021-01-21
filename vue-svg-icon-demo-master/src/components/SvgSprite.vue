<template>
  <!-- $options 包含直接附加到我们Vue组件的属性。 -->
  <!-- 我们附加svgSprite到组件data，不需要Vue为此设置响应性，因为SVG加载器仅在构建应用程序时运行 -->
  <svg width="0" height="0" style="display: none" v-html="$options.svgSprite" />
</template>

<script>
// 检索所有SVG文件并在使用时对其进行清理。
// 我们使用 感叹号! 来将资源文件与loaders分开，使用多个loaders，应在所有的转换规则(loader)之前加上感叹号!
const svgContext = require.context(
  '!svg-inline-loader?' +
    'removeTags=true' + // remove title tags, etc.
    '&removeSVGTagAttrs=true' + // enable removing attributes
    '&removingTagAttrs=fill' + // remove fill attributes
    '!@/assets/icons', // search this directory
  true, // search subdirectories
  /\w+\.svg$/i // only include SVG files
)
// 为了将所有SVG元素嵌套在SVG精灵中，我们必须将它们从<svg>元素转换为SVG<symbol>元素。这就像更改标签并为每个标签赋予唯一性一样简单id，然后从文件名中提取该唯一性。
const symbols = svgContext.keys().map((path) => {
  // get SVG file content
  const content = svgContext(path)
  // extract icon id from filename
  const id = path.replace(/^\.\/(.*)\.\w+$/, '$1')
  // replace svg tags with symbol tags and id attribute
  return content
    .replace('<svg', `<symbol id="${id}"`)
    .replace('svg>', 'symbol>')
})
console.log(symbols);
export default {
  name: 'SvgSprite',
  svgSprite: symbols.join('\n'), // concatenate all symbols into $options.svgSprite
}
</script>

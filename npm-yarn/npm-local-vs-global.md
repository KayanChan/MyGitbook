### 全局安装 VS 本地安装
<table>
  <tr><th>安装方式</th><th>命令行(以安装webpack为例子)</th></tr>
  <tr>
    <td rowspan="2">全局安装</td><td>npm install -g webpack</td>
  </tr>
  <tr>
    <td>
    <ol>
      <li>安装模块到全局，不会在项目node_modules目录中保存模块包</li>
      <li><strong>不会</strong>将模块依赖写入 devDependencies或dependencies 节点</li>
      <li>运行 npm install 初始化项目时<strong>不会下载</strong>模块</li>
      <li>如果只是全局安装，<strong>不能直接通过require()的方式</strong>去引用模块，需要手动解决包路径的配置问题</li>
      <li>为了区别不同项目使用指定的包(版本不同)，保证模块之间的相互依赖，需要更改包名(webpack@4.6.1)区别每个项目正常运行</li>
    </ol>
    </td>
  </tr>
  <tr>
    <td rowspan="6">本地安装</td><td>npm install webpack</td>
  </tr>
    <tr>
    <td>
    <ol>
      <li>安装模块到项目node_modules目录下</li>
      <li><strong>不会</strong>将模块依赖写入 devDependencies或dependencies 节点</li>
      <li>运行 npm install 初始化项目时<strong>不会下载</strong>模块</li>
    </ol>
    </td>
  </tr>
  <tr>
    <td>npm install --save webpack(npm install -S webpack)</td>
  </tr>
  <tr>
    <td>
    <ol>
      <li>安装模块到项目node_modules目录下</li>
      <li>会将模块依赖写入<strong>dependencies</strong>节点</li>
      <li>运行npm install初始化项目时，会将模块下载到项目目录下</li>
      <li>运行npm install --production或者注明 NODE_ENV变量值为production时，会自动下载模块到node_modules目录中</li>
    </ol>
    </td>
  </tr>
  <tr>
    <td>npm install --save-dev webpack(npm install -D webpack)</td>
  </tr>
  <tr>
    <td>
    <ol>
      <li>安装模块到项目node_modules目录下</li>
      <li>会将模块依赖写入<strong>devDependencies</strong>节点</li>
      <li>运行npm install初始化项目时，会将模块下载到项目目录下</li>
      <li>运行npm install --production或者注明 NODE_ENV变量值为production时，会自动下载模块到node_modules目录中</li>
    </ol>
    </td>
  </tr>
</table>
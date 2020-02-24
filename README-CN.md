# Altizure SDK 离线部署

本教程提供一个完全离线使用Altizure三维浏览服务的基本案例。

## 开始运行
* 在网页根目录发布本地服务
    ```
    cd <path>/altizure-sdk-offline/
    python -m SimpleHTTPSERVER 8000
    ```
    * 更详细的资料介绍请参考 [3D SDK Quick Start](https://docs.altizure.cn/en/jssdk.html)

* 通过浏览器访问 `http://localhost:8000/index.html` 查看案例

## 文件结构
本案例已经提供一份数据供您测试，下载链接：
链接: https://pan.baidu.com/s/1tEEbjO2aC2OviDCV5_fdhQ  密码: sjhw

您可以直接查看此三维数据，或者更改为您自己的数据。如果使用自己的数据，请遵照原本的文件夹结构，将数据和配置文件放置在正确的位置。

```
project
│   README.md
│   index.html
│   crop_and_water.html
│
└───public
│   └───data
│       └───<PID_1>
│       │   │   apiinfo-<PID_1>.json
│       │   └───web
│       │       │   *.ab
│       │       │   *.ab
│       │       │   ...
│       │       │   info.txt
│       └───<PID_2>
│       │   │   apiinfo-<PID_2>.json
│       │   │   crop_mask_<PID_2>.json (if it has)
│       │   │   water_mask_<PID_2>.json (if it has)
│       │   └───web
│       │       │   *.ab
│       │       │   *.ab
│       │       │   ...
│       │       │   info.txt
│       │   ...
│   
└───assets
│   └───img
│       └───waternormals.jpg
│   
└───js
    │   altizure-all.min.js
    │   altizure.min.js
```

+ `index.html` 是基本页，包含json配置文件的请求和模型加载代码。
+ `public\data\<PID>\web` 存储了altizure三维模型的二进制数据。文件夹内部一般是由多个 `.ab` 文件和一个 `info.txt` 组成。
+ `public\data\<PID>\apiinfo-<PID>.json` 存储了 altizure graphql api `project(<PID>)` 数据。
+ `public\data\<PID>\crop_mask_<PID>.json` 存储了模型裁剪数据。
+ `public\data\<PID>\water_mask_<PID>.json` 存储了模型水面数据。
+ `public\js\altizure.min.js` 是基本的 SDK 库， `public\js\altizure-all.min.js` 包含所有 plugins 的 SDK 库。


## 如何托管您自己的数据


* 保存您的 `.ab` 数据文件和 `info.txt` 文件到 `public\data\<PID>\web\` 目录中。 `.ab` 文件可以通过[Altizure 桌面端](https://www.altizure.cn/desktop)上的模型同步功能下载。
* `public\data\<PID>\apiinfo-<PID>.json` 文件中, 更改 `dataUrl` 中的 `<REPLACE_WITH_YOUR_HOSTNAME_PORT>` 为您的域名和端口，比如： `localhost:8000`。 
* `apiinfo-<PID>.json` 文件可以通过 altizure 官网 overview 页面下载: https://www.altizure.cn/overview?pid=PID
* 在 `index.html` 中修改您的 `apiinfo-<PID>.json` 文件请求路径。如果您完全按教程上面的文件夹结构放置数据，您只需修改PID为您自己的即可。
* 如果您需要加载模型的水面和裁剪，请参考 `crop_and_water.html` 案例。你需要从模型overview页面下载 `crop_mask_<PID>.json` 和 `water_mask_<PID>.json`, 将它们放置在 `data\<PID>` 目录下，并且修改 `crop_and_water.html` 中的 `<PID>` 为您项目的。

![project with crop and water](./public/assets/img/screen_capture.jpg)
* 如果您需要在您的场景中添加多个模型，您需要为每个模型使用独立的 `apiinfo`。 参照当前 `index.html` 中的方法，请求多个不同的 `apiinfo-<PID>.json` 文件，然后用这些apiinfo将多个模型添加到场景中。
\# 編譯與建構指南（build-guide.md）



本文件說明如何將本專案的 JSON 語法庫

包裝成「可編譯、可被其他程式載入」的 DLL / SO / 分析工具。



本指南為選用功能：

\- 如果你只想編輯 JSON，請參考 edit-guide.nd

\- 如果你要建立可被外部程式載入的語法工具，請參考本文件





-------------------------------------------------------------

\# 1. 必要工具



若你要將本專案變成「可編譯、可被載入的語言庫」，

建議安裝以下開發工具：



Windows：

\- Visual Studio 2019/2022（含 C++）

\- 或 MinGW-w64



Linux：

\- g++ 9+

\- cmake



macOS：

\- Xcode（clang）

\- cmake



所有平台：

\- nlohmann-json（用於讀取 JSON）

\- Git（取得來源碼）





-------------------------------------------------------------

\# 2. 建立必要的檔案（範本）



若要讓專案可編譯，你需要新增：



/include/

&nbsp;   yourlang.h          ← 提供外部使用的 API



/src/

&nbsp;   loader.cpp          ← 載入 JSON

&nbsp;   tokenizer.cpp       ← 可選：語法分詞

&nbsp;   parser.cpp          ← 可選：基本解析器

&nbsp;   yourlang.cpp        ← DLL 的入口



CMakeLists.txt          ← 編譯設定檔案



這些檔案不包含在主專案中，

因為此專案主要用途為「語法 JSON 資料庫」。





-------------------------------------------------------------

\# 3. JSON 檔案位置



語法庫（json 資料夾）在編譯後仍會被 DLL 使用：



/json/

&nbsp;   html.json

&nbsp;   css.json

&nbsp;   js.json

&nbsp;   py.json

&nbsp;   ccpp.json

&nbsp;   cpu.json

&nbsp;   gpu.json

&nbsp;   ...



因此，在 DLL 或 EXE 執行時，

請確保 JSON 路徑結構不變。





-------------------------------------------------------------

\# 4. 建立 CMakeLists.txt（範本）



若你想建構 DLL，可使用以下範本：



cmake\_minimum\_required(VERSION 3.10)

project(yourlang)



set(CMAKE\_CXX\_STANDARD 17)



add\_library(yourlang SHARED

&nbsp;   src/yourlang.cpp

&nbsp;   src/loader.cpp

)



target\_include\_directories(yourlang PUBLIC include)



find\_package(nlohmann\_json REQUIRED)

target\_link\_libraries(yourlang PRIVATE nlohmann\_json::nlohmann\_json)





-------------------------------------------------------------

\# 5. 編譯方式（跨平台）



mkdir build

cd build

cmake ..

cmake --build .



產生於：



Windows：

&nbsp;   yourlang.dll



Linux：

&nbsp;   libyourlang.so



macOS：

&nbsp;   libyourlang.dylib





-------------------------------------------------------------

\# 6. 如何在程式中載入這個 DLL（選用）



C++：



\#include "yourlang.h"

yl\_init();

yl\_tokenize("int x = 0;");



Python：



import ctypes

lib = ctypes.CDLL("yourlang.dll")

lib.yl\_init()



Node.js：



const ffi = require("ffi-napi");

const lib = ffi.Library("./yourlang", { yl\_init: \["void", \[]] });





-------------------------------------------------------------

\# 7. 不需要完整語言引擎也能使用



如果你只想讓外部程式讀取你的 JSON：



你可以使用任何語言（Python / JS / C++）直接讀取 JSON：



Python：

import json

data = json.load(open("json/cpu.json"))



Node.js：

const data = require("./json/cpu.json");



C++（nlohmann/json）：

json data = json::parse(std::ifstream("json/cpu.json"));





-------------------------------------------------------------

\# 8. 結語



本指南提供「若你想讓語法資料庫變成可編譯工具」的架構。

但本專案本身仍然可以僅作為：



\- 語法庫

\- 資料庫

\- 分析引擎的資料來源



使用者可自行選擇是否要建構 DLL 或語言引擎。




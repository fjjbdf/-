# -
海角社区视频破解获取地址：hjv58.top
// ==UserScript==
// @name 海角社区破解版
// @version 3.3.5
// @description 🔥免费看付费视频，下载视频，复制播放链接，
// @namespace 海角社区
// @author xxx
// @include *://hj*.*/*
// @include *://*.hj*.*/*
// @include *://*.hai*.*/*
// @include *://hai*.*/*
// @include *://hj*/*
// @include *://*.hj*/*
// @include
// @include
// @include */post/details/*
// @include *://blog.luckly-mjw.cn/*
// @include *://tools.thatwind.com/*
// @include *://tools.bugscaner.com/*
// @match *://*/post/details*
// @require https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js
// @require https://cdnjs.cloudflare.com/ajax/libs/hls.js/1.5.8/hls.min.js
// @require https://cdnjs.cloudflare.com/ajax/libs/dplayer/1.27.1/DPlayer.min.js
// @run-at document-start
// @grant unsafeWindow
// @grant GM_addStyle
// @grant GM_getValue
// @grant GM_setValue
// @grant GM_getResourceText
// @grant GM_xmlhttpRequest
// @charset UTF-8
// @antifeature payment
// @license MIT
// ==/UserScript==
const u = "WVVoU01HTkViM1pNTW1oeFkzcG5kV1JIT1hjPQ==";
var targetNode = document.documentElement;
var config = { attributes: true, childList: true, subtree: true };

var observer = new MutationObserver(function (mutationsList, observer) {
  mutationsList.forEach(function (mutation) {
    if (mutation.target.tagName !== "TITLE") {
      var divElement = document.querySelector(
        "div.nickname > span:first-child + span"
      );
      if (divElement) {
        // 获取网址
        var currentURL = window.location.href;
        if (currentURL.includes("last")) {
          var minititle = "最新帖子";
        } else if (currentURL.includes("essence")) {
          var minititle = "精华帖子";
        } else if (currentURL.includes("reward")) {
          var minititle = "悬赏帖子";
        } else if (currentURL.includes("sell")) {
          var minititle = "出售帖子";
        } else {
          var minititle = "全部帖子";
        }
        var nickname = divElement.previousElementSibling.textContent;
        var idInfo = divElement.textContent;
        document.title = nickname + "的" + minititle + "-海角社区";
      }
      //______________________________________________________________

      //帖子的标题修改
      var relativeH2 = document.querySelector("h2 span");
      if (relativeH2) {
        var text = relativeH2.textContent;
        var parentElement = document.querySelector(
          "span a.hjbox-linkcolor"
        ).parentNode;
        if (parentElement) {
          var keyword = parentElement.textContent.trim();
          document.title = text + "_" + keyword + "-海角社区";
        }
      }
      //______________________________________________________________

      //首页标题
      var liElements = document.querySelectorAll("li.menu-li.menu-item");
      var keywords = [];
      liElements.forEach(function (liElement) {
        var linkElement = liElement.querySelector("a.menu-link");

        if (linkElement && linkElement.classList.contains("visible")) {
          var keyword =
            linkElement.querySelector("span:last-child").textContent;
          keywords.push(keyword);
        }
      });

      if (keywords.length > 0) {
        document.title = keywords.join(", ") + "-海角社区";

        var visibleKeywordElements = document.querySelectorAll(
          "li div.child_link.lahjyu.visible"
        );
        var visibleKeywords = [];
        visibleKeywordElements.forEach(function (visibleKeywordElement) {
          var visibleKeyword = visibleKeywordElement.textContent.trim();
          visibleKeywords.push(visibleKeyword);
        });
        if (visibleKeywords.length > 0) {
          var cleanedValue = visibleKeywords
            .join(", ")
            .replace(/\s*VIP\d*\s*/g, "");
          document.title =
            keywords.join(", ") + "-" + cleanedValue + "-海角社区";

          var activeTitle = document.querySelector(".active a");
          if (activeTitle) {
            var titleText = activeTitle.textContent.trim();
            document.title =
              keywords.join(", ") +
              "-" +
              cleanedValue +
              "-" +
              titleText +
              "-海角社区";
          }
        }

        var activeTitle = document.querySelector(".title.active");
        if (activeTitle) {
          var titleText = activeTitle.textContent.trim();
          document.title = keywords.join(", ") + titleText + "-海角社区";
        }
      }
      //______________________________________________________________

      //发帖时标题
      var hasDraft = document.querySelector(".draft") !== null;
      var hasSubmitBtn = document.querySelector(".common-submitBtn") !== null;
      var hasNotice =
        document.querySelector(
          'span[style="font-size: 12px; color: rgb(255, 101, 101);"]'
        ) !== null;

      var result = "";

      if (hasDraft && hasSubmitBtn && hasNotice) {
        result = "发帖";
        document.title = result + "-海角社区";
      }
      //______________________________________________________________
    }

    var tidioChatDiv = document.getElementById("tidio-chat");
    if (tidioChatDiv) {
      tidioChatDiv.remove();
    }
  });
});

observer.observe(targetNode, config);

var scriptName = "mdui.min.js"; // 指定脚本文件名
if (!hasScriptInSourceCode(scriptName)) {
  var cssLink = document.createElement("link");
  cssLink.rel = "stylesheet";

  cssLink.href = "https://unpkg.com/mdui@1.0.2/dist/css/mdui.min.css";;
  var jsScript = document.createElement("script");
  jsScript.src = "https://unpkg.com/mdui@1.0.2/dist/js/mdui.min.js";;

  document.head.appendChild(cssLink);
  document.head.appendChild(jsScript);
}
// 判断网页源代码是否包含指定的脚本文件
function hasScriptInSourceCode(scriptName) {
  var sourceCode = document.documentElement.innerHTML;
  return sourceCode.includes(scriptName);
}

// 创建按钮元素
var buttonElement = document.createElement("button");
buttonElement.className = "mdui-fab mdui-fab-fixed mdui-ripple mdui-color-pink";
var iconElement = document.createElement("i");
iconElement.className = "mdui-icon material-icons";
iconElement.textContent = "arrow_upward";
buttonElement.appendChild(iconElement);
var body = document.body;
body.appendChild(buttonElement);
// 添加按钮点击事件
buttonElement.addEventListener("click", function () {
  window.scrollTo({ top: 0, behavior: "smooth" });
});

function findTargetElement(targetContainer, maxTryTime = 30) {
  const body = window.document;
  let tabContainer;
  let tryTime = 0;
  let startTimestamp;
  return new Promise((resolve, reject) => {
    function tryFindElement(timestamp) {
      if (!startTimestamp) {
        startTimestamp = timestamp;
      }
      const elapsedTime = timestamp - startTimestamp;
      if (elapsedTime >= 500) {
        console.log(
          "find element：" + targetContainer + "，this" + tryTime + "num"
        );
        tabContainer = body.querySelector(targetContainer);
        if (tabContainer) {
          resolve(tabContainer);
        } else if (++tryTime === maxTryTime) {
          reject();
        } else {
          startTimestamp = timestamp;
        }
      }
      if (!tabContainer && tryTime < maxTryTime) {
        requestAnimationFrame(tryFindElement);
      }
    }
    requestAnimationFrame(tryFindElement);
  });
}

function shiowTips() {
  GM_addStyle(`
      #my-mask{
       position: fixed;
       top:0;
       left:0;
       right:0;
       bottom:0;
       background-color: #0000004d;
       z-index: 999999;
      }
      #my-container{
       position: absolute;
       top: 50%;
       left: 50%;
       transform: translate(-50%, -50%);
       width: 70%;
       border-radius: 15px;
       background-color: white;
       padding: 10px 15px;
       z-index: 999998;
      }
      #my-container .title{
显示:块；
字体大小:20px；
颜色:#222；
字体重量:500；
文本对齐:中心；
边距：10 px 0；
      }
#我的容器.内容{
颜色：#66a6a6a
字母间距：2像素；
字体大小：15像素；
线高：22像素；
      }
#我的容器.btn{
显示:块；
      }
#我的容器.btn boutton{
显示:块；
边距:10px 自动；
边距顶部:30px；
宽度:82像素；
高度:35像素；
边缘半径:30px；
边框:无；
颜色:白色；
过渡:所有0.3秒都轻松；
背景颜色:#ec407a；
线高:35像素；
文本对齐:中心；
      }
     `// @3.3.5版
// @描述🔥免费看付费视频，下载视频，复制播放链接，
// @名称空间海角社区`
<div 身份证件="我的面具">
<div 身份证件="我的集装箱">
公告《查看类=标题》
<视角班级="内容">
          抱歉，此脚本为付费脚本，请通过链接${atob（
atob（atob（u））
          )}购买后安装最新版本脚本再使用，谢谢!
</视角>
<视角班级="按钮">
          <博顿>去购买</博顿>
</视角>
</div>
</div>
      `// @匹配 *://*/帖子/详情*
// @要求 https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js
// @要求 https://cdnjs.cloudflare.com/ajax/libs/hls.js/1.5.8/hls.min.js
// @要求 https://cdnjs.cloudflare.com/ajax/libs/dplayer/1.27.1/DPlayer.min.js
// @在文档启动时运行
// @授予不安全窗口
// @授予 GM_addStyle
// @授予 GM_getValue
// @授予 GM_setValue


<!DOCTYPE html>
<html lang='zh-CN'>
<head>
<title>21-k8s详细教程/Kubernetes详细教程.md · yooome/LearningNotes - Gitee</title>
<meta content='on' http-equiv='x-dns-prefetch-control'>
<link href='//e.gitee.com' rel='dns-prefetch'>
<link href='//files.gitee.com' rel='dns-prefetch'>
<link href='//toscode.gitee.com' rel='dns-prefetch'>
<link href='https://cn-assets.gitee.com' rel='dns-prefetch'>
<link rel="shortcut icon" type="image/vnd.microsoft.icon" href="https://cn-assets.gitee.com/assets/favicon-9007bd527d8a7851c8330e783151df58.ico" />
<link rel="canonical" href="https://gitee.com/yooome/golang" />
<meta content='gitee.com/yooome/golang git https://gitee.com/yooome/golang.git' name='go-import'>
<meta charset='utf-8'>
<meta content='always' name='referrer'>
<meta content='Gitee' property='og:site_name'>
<meta content='Object' property='og:type'>
<meta content='https://gitee.com/yooome/golang/blob/main/21-k8s%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B/Kubernetes%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B.md' property='og:url'>
<meta content='https://gitee.com/static/images/logo_themecolor.png' itemprop='image' property='og:image'>
<meta content='21-k8s详细教程/Kubernetes详细教程.md · yooome/LearningNotes - Gitee' itemprop='name' property='og:title'>
<meta content='各位小伙伴，k8s 中的违规内容已经做了修复，你们可以正常使用了。gitee 这个老六，给你提示违规信息，却不给你提供那些词违规了，真的服了这个老六了，现在已经处理完了。gitee是有自己的敏感词汇检测机制，感觉很不智能。大家在写技术博客的时候注意用词，避免不必要的麻烦。大家有什么问题可以+v: yooobee 来讨论。' property='og:description'>
<meta content='码云,Gitee,代码托管,Git,Git@OSC,Gitee.com,开源,内源,项目管理,版本控制,开源代码,代码分享,项目协作,开源项目托管,免费代码托管,Git代码托管,Git托管服务' name='Keywords'>
<meta content='各位小伙伴，k8s 中的违规内容已经做了修复，你们可以正常使用了。gitee 这个老六，给你提示违规信息，却不给你提供那些词违规了，真的服了这个老六了，现在已经处理完了。gitee是有自己的敏感词汇检测机制，感觉很不智能。大家在写技术博客的时候注意用词，避免不必要的麻烦。大家有什么问题可以+v: yooobee 来讨论。' itemprop='description' name='Description'>
<meta content='pc,mobile' name='applicable-device'>

<meta content="IE=edge" http-equiv="X-UA-Compatible" />
<meta name="csrf-param" content="authenticity_token" />
<meta name="csrf-token" content="rdbHfbHaUAMX6skCC+Fhjox2lNnySr3cHkl/diOGfg328lDWTkWX45q7uJDScDpBFApWnfRJEq2/b5bt8sJ1ig==" />

<link rel="stylesheet" media="all" href="https://cn-assets.gitee.com/assets/application-f708e90a15df8fcad5c5a86525fba4d1.css" />
<script>
//<![CDATA[
window.gon = {};gon.locale="en";gon.sentry_dsn=null;gon.baidu_register_hm_push=null;gon.info={"controller_path":"blob","action_name":"show","current_user":false};gon.tour_env={"current_user":null,"action_name":"show","original_url":"https://gitee.com/yooome/golang/blob/main/21-k8s%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B/Kubernetes%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B.md","controller_path":"blob"};gon.http_clone="https://gitee.com/yooome/golang.git";gon.user_project="yooome/golang";gon.manage_branch="Manage branch";gon.manage_tag="Manage tag";gon.enterprise_id=0;gon.create_reaction_path="/yooome/golang/reactions";gon.ipipe_base_url="https://go-api.gitee.com";gon.artifact_base_url="https://go-repo.gitee.com";gon.gitee_go_remote_url="https://go.gitee.com/assets";gon.gitee_go_active=false;gon.current_project_is_mirror=false;gon.show_repo_comment=false;gon.diagram_viewer_path="https://diagram-viewer.giteeusercontent.com";gon.ent_host="e.gitee.com";gon.ref="main";
//]]>
</script>
<script src="https://cn-assets.gitee.com/assets/application-1a4bf2ba7b1e19f0f3f7b1bf63122b0b.js"></script>
<script src="https://cn-assets.gitee.com/assets/lib/jquery.timeago.en-d8a06c79c6bf9e7618c1ade936096da5.js"></script>

<link rel="stylesheet" media="all" href="https://cn-assets.gitee.com/assets/projects/application-46b94c31ba11ae8c37eacce2bdb5603e.css" />
<script src="https://cn-assets.gitee.com/assets/projects/app-621ae6d8ca6946832ee317e426aa86d8.js"></script>

<script type='text/x-mathjax-config'>
MathJax.Hub.Config({
  tex2jax: {
    inlineMath: [['$','$'], ['\\(','\\)']],
    displayMath: [["$$","$$"],["\\[","\\]"]],
    processEscapes: true,
    skipTags: ['script', 'noscript', 'style', 'textarea', 'pre', 'code'],
    ignoreClass: "container|files",
    processClass: "markdown-body"
  }
});
</script>
<script src="https://cn-assets.gitee.com/uploads/resources/MathJax-2.7.2/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>

<script>
  (function () {
    var messages = {
      'zh-CN': {
        addResult: '增加 <b>{term}</b>',
        count: '已选择 {count}',
        maxSelections: '最多 {maxCount} 个选择',
        noResults: '未找到结果',
        serverError: '连接服务器时发生错误'
      },
      'zh-TW': {
        addResult: '增加 <b>{term}</b>',
        count: '已選擇 {count}',
        maxSelections: '最多 {maxCount} 個選擇',
        noResults: '未找到結果',
        serverError: '連接服務器時發生錯誤'
      }
    }
  
    if (messages[gon.locale]) {
      $.fn.dropdown.settings.message = messages[gon.locale]
    }
  }());
</script>

<script>
  var userAgent = navigator.userAgent;
  var isLessIE11 = userAgent.indexOf('compatible') > -1 && userAgent.indexOf('MSIE') > -1;
  if(isLessIE11){
    var can_access = ""
    if (can_access != "true"){
      window.location.href = "/incompatible.html";
    }
  }
  document.addEventListener("error", function (ev) {
    var elem = ev.target;
    if (elem.tagName.toLowerCase() === 'img') {
      elem.src = "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAMgAAADICAAAAACIM/FCAAACh0lEQVR4Ae3ch5W0OgyG4dt/mQJ2xgQPzJoM1m3AbALrxzrf28FzsoP0HykJEEAAAUQTBBBAAAEEEEAAAQQQQAABBBBAAAEEEEAAAQQQQAABBBBAAAEEkKK0789+GK/I2ezfQB522PnS1qc8pGgXvr4tE4aY0XOUWlGImThWgyCk6DleixzE7qwBkg/MGiDPlVVAyp1VQGrPKiACDhFI6VkF5LmzCki+sg7IwDoglnVAil0IMkeG9CyUiwsxLFUVFzJJOQaKCjFCDN9RXMjIX7W6ztZXZDKKCyn8sWJvH+nca7WHDN9lROlAliPH9iRKCPI4cswFJQWxB46toLQgQ9jhn5QYZA9DOkoMUoQde5YapAxDWkoNYsOQR3KQd9CxUnIQF4S49CB9ENKlBxmDEKsFUgMCCCCAAHIrSF61f6153Ajy8nyiPr8L5MXnmm4CyT2fzN4DUvHZ+ntA2tOQBRBAAAEEEEAAAQQQ7ZBaC6TwSiDUaYHQ2yuB0MN+ft+43whyrs4rgVCjBUKTFshLC6TUAjGA3AxSaYFYLZBOC2RUAsk8h5qTg9QcbEoOsoQhQ2qQhsO5xCD5dgB5JQaZ+KBKGtKecvR81Ic0ZDjByKdDx0rSEDZ/djQbH+bkIdvfJFm98BfV8hD2zprfVdlu9PxVeyYAkciREohRAplJCaRSAplJCcQogTjSAdlyHRBvSAekJR0QRzogA+mADJkOiCPSAPEtqYBshlRAXC43hxix2QiOuEZkVERykGyNo9idIZKE0HO7XrG6OiMShlDWjstVzdPgXtUH9v0CEidAAAEEEEAAAQQQQAABBBBAAAEEEEAAAQQQQAABBBBAAAEEEEAAAQQQQP4HgjZxTpdEii0AAAAASUVORK5CYII=";
    }
  }, true);
</script>
</head>

<script src="//res.wx.qq.com/open/js/jweixin-1.2.0.js"></script>
<script>
  var title = document.title.replace(/( - Gitee| - 码云)$/, '')
      imgUrl = '';
  
  document.addEventListener('DOMContentLoaded', function(event) {
    var imgUrlEl = document.querySelector('.readme-box .markdown-body > img, .readme-box .markdown-body :not(a) > img');
    imgUrl = imgUrlEl && imgUrlEl.getAttribute('src');
  
    if (!imgUrl) {
      imgUrlEl = document.querySelector('meta[itemprop=image]');
      imgUrl = imgUrlEl && imgUrlEl.getAttribute('content');
      imgUrl = imgUrl || "https://gitee.com/static/images/logo_themecolor.png";
    }
  
    wx.config({
      debug: false,
      appId: "wxff219d611a159737",
      timestamp: "1749598464",
      nonceStr: "6f88c18f12a258119f58490c3e4a0974",
      signature: "ea796cc4ffe76c977c3866360aa8dfe2e2ef4981",
      jsApiList: [
        'onMenuShareTimeline',
        'onMenuShareAppMessage'
      ]
    });
  
    wx.ready(function () {
      wx.onMenuShareTimeline({
        title: title, // 分享标题
        link: "https://gitee.com/yooome/golang/blob/main/21-k8s%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B/Kubernetes%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B.md", // 分享链接，该链接域名或路径必须与当前页面对应的公众号JS安全域名一致
        imgUrl: imgUrl // 分享图标
      });
      wx.onMenuShareAppMessage({
        title: title, // 分享标题
        link: "https://gitee.com/yooome/golang/blob/main/21-k8s%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B/Kubernetes%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B.md", // 分享链接，该链接域名或路径必须与当前页面对应的公众号JS安全域名一致
        desc: document.querySelector('meta[name=Description]').getAttribute('content'),
        imgUrl: imgUrl // 分享图标
      });
    });
    wx.error(function(res){
      console.error('err', res)
    });
  })
</script>

<body class='blob-site-content blob_show git-project lang-en'>
<header class='common-header fixed noborder' id='git-header-nav'>
<div class='ui container'>
<div class='ui menu header-menu header-container'>
<div class='git-nav-expand-bar'>
<i class='iconfont icon-mode-table'></i>
</div>
<div class='gitee-nav__sidebar'>
<div class='gitee-nav__sidebar-container'>
<div class='gitee-nav__sidebar-top'>
<div class='gitee-nav__avatar-box'></div>
<div class='gitee-nav__buttons-box'>
<a class="ui button small fluid orange" href="/login">Sign in</a>
<a class="ui button small fluid basic is-register" href="/signup">Sign up</a>
</div>
</div>
<div class='gitee-nav__sidebar-middle'>
<div class='gitee-nav__sidebar-list'>
<ul>
<li class='gitee-nav__sidebar-item'>
<a href="/explore"><i class='iconfont icon-ic-discover'></i>
<span class='gitee-nav__sidebar-name'>Explore</span>
</a></li>
<li class='gitee-nav__sidebar-item'>
<a href="/enterprises"><i class='iconfont icon-ic-enterprise'></i>
<span class='gitee-nav__sidebar-name'>Enterprise</span>
</a></li>
<li class='gitee-nav__sidebar-item'>
<a href="/education"><i class='iconfont icon-ic-education'></i>
<span class='gitee-nav__sidebar-name'>Education</span>
</a></li>
<li class='gitee-nav__sidebar-item split-line'></li>
<li class='gitee-nav__sidebar-item'>
<a href="/search"><i class='iconfont icon-ic-search'></i>
<span class='gitee-nav__sidebar-name'>Search</span>
</a></li>
<li class='gitee-nav__sidebar-item'>
<a href="/help"><i class='iconfont icon-help-circle'></i>
<span class='gitee-nav__sidebar-name'>Help</span>
</a></li>
<li class='gitee-nav__sidebar-item'>
<a href="/terms"><i class='iconfont icon-file'></i>
<span class='gitee-nav__sidebar-name'>Terms of use</span>
</a></li>
<li class='gitee-nav__sidebar-item'>
<a href="/about_us"><i class='iconfont icon-issuepx'></i>
<span class='gitee-nav__sidebar-name'>About Us</span>
</a></li>
</ul>
</div>
</div>
<div class='gitee-nav__sidebar-bottom'>
<div class='gitee-nav__sidebar-close-button'>
<i class='fa fa-angle-double-left'></i>
</div>
</div>
</div>
</div>

<!-- /todo 10周年活动结束后 恢复 -->
<div class='item gitosc-logo'>
<a href="https://gitee.com"><img alt='Gitee — A Git-based Code Hosting and Research Collaboration Platform' class='ui inline image' height='28' src='/static/images/logo.svg?t=158106664' title='Gitee — A Git-based Code Hosting and Research Collaboration Platform' width='95'>
<img alt='Gitee — A Git-based Code Hosting and Research Collaboration Platform' class='ui inline black image' height='28' src='/static/images/logo-black.svg?t=158106664' title='Gitee — A Git-based Code Hosting and Research Collaboration Platform' width='95'>
</a></div>
<a title="Explore" class="item " href="/explore">Explore
</a><a title="Enterprise" class="item " href="/enterprises">Enterprise
</a><a title="Education" class="item " href="/education">Education
</a><a title="Gitee Premium" class="item" target="_blank" href="https://gitee.cn?utm_source=giteecom">Gitee Premium
</a><a title="Gitee AI" class="item" id="gitee-blog" target="_blank" href="https://ai.gitee.com/serverless-api/?utm_sources=site_nav"><span>
Gitee AI
</span>
<img alt='Gitee AI' class='ui inline image' src='/static/images/notification-star.svg' style='transform: translate(-4px, -8px)' title='Gitee AI'>
</a><div class='center responsive-logo'>
<a href="https://gitee.com"><img alt='Gitee — A Git-based Code Hosting and Research Collaboration Platform' class='ui inline image' height='24' src='/static/images/logo.svg?t=158106664' title='Gitee — A Git-based Code Hosting and Research Collaboration Platform' width='85'>
<img alt='Gitee — A Git-based Code Hosting and Research Collaboration Platform' class='ui inline black image' height='24' src='/static/images/logo-black.svg?t=158106664' title='Gitee — A Git-based Code Hosting and Research Collaboration Platform' width='85'>
</a></div>
<div class='right menu userbar right-header' id='git-nav-user-bar'>
<form class="ui item" id="navbar-search-form" data-text-require="Search keywords can not be less than one" data-text-filter="Invalid search content" action="/search" accept-charset="UTF-8" method="get"><input name="utf8" type="hidden" value="&#x2713;" />
<input type="hidden" name="type" id="navbar-search-type" />
<input type="hidden" name="fork_filter" id="fork_filter" value="on" />
<div class='ui search header-search'>
<input type="text" name="q" id="navbar-search-input" value="" class="prompt" placeholder="Search" />
</div>
</form>

<script>
  var can_search_in_repo = 1,
      repo = "VFZSUk1rMUVUWHBOZWxab1RucFplbHBuUFQxaE56WXpaZz09YTc2M2Y=",
      reponame = "yooome/golang";
  
  $(function() {
    var $search = $('#navbar-search-form .ui.search');
    $search.search({
      apiSettings: {
        url: '/search/relative_project?q={query}',
        onResponse: function (res) {
          if (res && res.status === 200 && res.data) {
            var query = htmlSafe($search.search('get value'));
  
            res.data.map(function (item) {
              item.path_ns = '/' + item.path_ns;
              item.icon = 'iconfont icon-project-public';
            });
            res.data.unshift({
              name_ns: "在全站搜索 <b class='hl'>" + query +"</b> 相关项目",
              path_ns: '/search?fork_filter=on&q=' + query,
              icon: 'iconfont icon-search'
            });
            return res;
          } else {
            return { data: [] };
          }
        }
      },
      fields: {
        results: 'data',
        description: 'name_ns',
        url: 'path_ns',
        icon: 'icon'
      },
      minCharacters: 1,
      maxResults: 10,
      searchDelay: 250,
      showNoResults: false,
      transition: 'fade'
    });
  });
</script>

<div class='ui item' id='feature-update-notice'>
<div class='notice-update-icon'>
<a class="notice-update-popup click-knowed" title="" href="javascript:void(0)"><img alt="功能更新" title="" class="bubl_icon bubl-off-icon" src="https://cn-assets.gitee.com/assets/bulb_off-24ee940be20998aace89a3f040cbc704.svg" />
<img alt="功能更新" title="" class="bubl_icon bubl-on-icon" src="https://cn-assets.gitee.com/assets/bulb_on-3986b1dc417285398e3d15671bd8f261.svg" />
</a></div>
<div class='feature-update-notice-panel menu'>
<div class='notice-img'>
<img alt="" title="" class="notice-img-show" src="" />
</div>
<div class='notice-update-title'></div>
<div class='notice-update-des'></div>
<div class='notice-btn-list d-flex-between'>
<button name="button" type="button" class="ui basic orange button btn-notice btn-knowed click-knowed" style="margin-right: 0">I know</button>
<a class="ui button orange btn-notice btn-details click-knowed" target="_blank" href="">View Details</a>
</div>
</div>
</div>

<a class="item git-nav-user__login-item" href="/login">Sign in
</a><a class="item git-nav-user__register-item" href="/signup">Sign up
</a><script>
  $('.destroy-user-session').on('click', function() {
    $.cookie('access_token', null, { path: '/' });
  })
</script>

</div>
</div>
</div>
</header>
<script>
  Gitee.initNavbar()
  Gitee.initRepoRemoteWay()
  $.cookie('user_locale',null)
</script>

<script>
  var userAgent = navigator.userAgent;
  var isLessIE11 = userAgent.indexOf('compatible') > -1 && userAgent.indexOf('MSIE') > -1;
  if(isLessIE11){
    var can_access = ""
    if (can_access != "true"){
      window.location.href = "/incompatible.html";
    }
  }
</script>

<div class='fixed-notice-infos'>
<div class='all-messages'>
</div>
<div class='ui container'>
<div class='flash-messages' id='messages-container'></div>
</div>
<script>
  (function() {
    $(function() {
      var $error_box, alertTip, notify_content, notify_options, template;
      template = '<div data-notify="container" class="ui {0} message" role="alert">' + '<i data-notify="dismiss" class="close icon"></i>' + '<span data-notify="message">{2}</span>' + '</div>';
      notify_content = null;
      notify_options = {};
      alertTip = '';
      $error_box = $(".flash_error.flash_error_box");
      if (notify_options.type === 'error' && $error_box.length > 0 && !$.isEmptyObject(notify_content.message)) {
        if (notify_content.message === 'captcha_fail') {
          alertTip = "The captcha is incorrect";
        } else if (notify_content.message === 'captcha_expired') {
          alertTip = "The captcha was expired, please refresh it";
        } else if (notify_content.message === 'not_found_in_database') {
          alertTip = "Invalid email or password.";
        } else if (notify_content.message === 'not_found_and_show_captcha') {
          alertTip = "Invalid email or password.";
        } else if (notify_content.message === 'phone_captcha_fail') {
          alertTip = "The phone captcha is incorrect";
        } else {
          alertTip = notify_content.message;
        }
        return $error_box.html(alertTip).show();
      } else if (notify_content) {
        if ("show" === 'third_party_binding') {
          return $('#third_party_binding-message').html(notify_content.message).addClass('ui message red');
        }
        notify_options.delay = 3000;
        notify_options.template = template;
        notify_options.offset = {
          x: 10,
          y: 30
        };
        notify_options.element = '#messages-container';
        return $.notify(notify_content, notify_options);
      }
    });
  
  }).call(this);
</script>

</div>
<script>
  (function() {
    $(function() {
      var setCookie;
      setCookie = function(name, value) {
        $.cookie(name, value, {
          path: '/',
          expires: 365
        });
      };
      $('#remove-bulletin, #remove-bulletin-dashboard').on('click', function() {
        setCookie('remove_bulletin', "gitee-maintain-1749202263");
        $('#git-bulletin').hide();
      });
      $('#remove-member-bulletin').on('click', function() {
        setCookie('remove_member_bulletin', "gitee_member_bulletin");
        $(this).parent().hide();
      });
      return $('#remove-gift-bulletin').on('click', function() {
        setCookie('remove_gift_bulletin', "gitee-gift-bulletin");
        $(this).parent().hide();
      });
    });
  
  }).call(this);
</script>
<script>
  function closeMessageBanner(pthis, type, val) {
    var json = {}
  
    val = typeof val === 'undefined' ? null : val
    $(pthis).parent().remove()
    if (type === 'out_of_enterprise_member') {
      json = {type: type, data: val}
    } else if (type === 'enterprise_overdue') {
      json = {type: type, data: val}
    }
    $.post('/profile/close_flash_tip', json)
  }
</script>

<div class='project_detail site-content'>
<div class='git-project-header'>
<div class='fixed-notice-infos'>
<div class='ui info icon floating message green' id='fetch-ok' style='display: none'>
<div class='content'>
<div class='header status-title'>
<i class='info icon status-icon'></i>
Fetch the repository succeeded.
</div>
</div>
</div>
<div class='ui info icon floating message error' id='fetch-error' style='display: none'>
<div class='content'>
<div class='header status-title'>
<i class='info icon status-icon'></i>
<span class='error_msg'></span>
</div>
</div>
</div>
</div>
<div class='ui container'>

<div class='git-project-header-details'>
<div class='git-project-header-container'>
<div class='git-project-header-actions'>
<div class='ui tiny modal project-donate-modal' id='project-donate-modal'>
<i class='iconfont icon-close close'></i>
<div class='header'>Donate</div>
<div class='content'>
Please sign in before you donate.
</div>
<div class='actions'>
<a class='ui blank button cancel'>Cancel</a>
<a class='ui orange ok button' href='/login'>Sign in</a>
</div>
</div>
<div class='ui small modal wepay-qrcode'>
<i class='iconfont icon-close close'></i>
<div class='header'>
Scan WeChat QR to Pay
<span class='wepay-cash'></span>
</div>
<div class='content weqcode-center'>
<img id='wepay-qrcode' src=''>
</div>
<div class='actions'>
<div class='ui cancel blank button'>Cancel</div>
<div class='ui ok orange button'>Complete</div>
</div>
</div>
<div class='ui mini modal' id='confirm-alipay-modal'>
<div class='header'>Prompt</div>
<div class='content'>
Switch to Alipay.
</div>
<div class='actions'>
<div class='ui approve orange button'>OK</div>
<div class='ui blank cancel button'>Cancel</div>
</div>
</div>

<span class='ui buttons basic watch-container'>
<div class='ui dropdown button js-project-watch' data-watch-type='unwatch'>
<input type='hidden' value=''>
<i class='iconfont icon-watch'></i>
<div class='text'>
Watch
</div>
<i class='dropdown icon'></i>
<div class='menu'>
<a data-value="unwatch" class="item" rel="nofollow" data-method="post" href="/yooome/golang/unwatch"><i class='iconfont icon-msg-read'></i>
Unwatch
</a><a data-value="watching" class="item" rel="nofollow" data-method="post" href="/yooome/golang/watch"><i class='iconfont icon-msg-read'></i>
Watching
</a><a data-value="releases_only" class="disabled item" rel="nofollow" data-method="post" href="/yooome/golang/release_only_watch"><i class='iconfont icon-msg-read'></i>
Releases Only
</a><a data-value="ignoring" class="item" rel="nofollow" data-method="post" href="/yooome/golang/ignoring_watch"><i class='iconfont icon-msg-read'></i>
Ignoring
</a></div>
</div>
<style>
  .js-project-watch .text .iconfont {
    display: none; }
  .js-project-watch a, .js-project-watch a:hover {
    color: #000; }
  .js-project-watch .item > .iconfont {
    visibility: hidden;
    margin-left: -10px; }
  .js-project-watch .selected .iconfont {
    visibility: visible; }
  .js-project-watch .menu {
    margin-top: 4px !important; }
</style>
<script>
  $('.js-project-watch').dropdown({
    action: 'select',
    onChange: function(value, text, $selectedItem) {
      var type = value === 'unwatch' ? 'Watch' : 'Watching';
      $(this).children('.text').text(type);
      $(this).dropdown('set selected', value)
    }
  });
</script>

<a class="ui button action-social-count" title="133" href="/yooome/golang/watchers">133
</a></span>
<span class='basic buttons star-container ui'>
<a class="ui button star" href="/login"><i class='iconfont icon-star'></i>
Star
</a><a class="ui button action-social-count " title="1641" href="/yooome/golang/stargazers">1.6K
</a></span>
<span class='ui basic buttons fork-container' title='You do not have the permission to fork this repository'>
<a class="ui button fork" title="You must be signed in to fork a repository" href="/login"><i class='iconfont icon-fork'></i>
Fork
</a><a class="ui button action-social-count disabled-style" title="1909" href="/yooome/golang/members">1.9K
</a></span>
</div>
<h2 class='git-project-title mt-0 mb-0'>
<span class="project-title"><i class="project-icon iconfont icon-project-public" title="This is a public repository"></i> <a title="yooome" class="author" href="/yooome">yooome</a>/<a title="LearningNotes" class="repository" target="" style="padding-bottom: 0px; margin-right: 4px" href="/yooome/golang">LearningNotes</a></span><span class="project-badges"><style>
  .gitee-modal {
    width: 500px !important; }
</style>
</span>
<input type="hidden" name="project_title" id="project_title" value="yooome/LearningNotes" />
</h2>
</div>
</div>
</div>
<script>
  var title_import_url = "false";
  var title_post_url = "/yooome/golang/update_import";
  var title_fork_url = "/yooome/golang/sync_fork";
  var title_project_path = "golang";
  var title_p_name = "LearningNotes";
  var title_p_id= "14603335";
  var title_description = "各位小伙伴，k8s 中的违规内容已经做了修复，你们可以正常使用了。gitee 这个老六，给你提示违规信息，却不给你提供那些词违规了，真的服了这个老六了，现在已经处理完了。gitee是有自己的敏感词汇检测机制，感觉很不智能。大家在写技术博客的时候注意用词，避免不必要的麻烦。大家有什么问题可以+v: yooobee 来讨论。";
  var title_form_authenticity_token = "JZ9QxFNDFiLsm0aISH4kKRjHGk03lrns43TaG9vTq0B+u8dvrNzRwmHKNxqR73/mgLvYCTGVFp1CUjOACpegxw==";
  var watch_type = "unwatch";
  var checkFirst = false;
  
  $('.js-project-watch').dropdown('set selected', watch_type);
  $('.checkbox.sync-wiki').checkbox();
  $('.checkbox.sync-prune').checkbox();
  $('.checkbox.team-member-checkbox').checkbox();
</script>
<style>
  i.loading, .icon-sync.loading {
    -webkit-animation: icon-loading 1.2s linear infinite;
    animation: icon-loading 1.2s linear infinite;
  }
  .qrcode_cs {
    float: left;
  }
  .check-sync-wiki {
    float: left;
    height: 28px;
    line-height: 28px;
  }
  .sync-wiki-warn {
    color: #e28560;
  }
</style>

<div class='git-project-nav'>
<div class='ui container'>
<div class='ui secondary pointing menu'>
<a class="item active " href="/yooome/golang"><i class='iconfont icon-code'></i>
Code
</a><a class="item " href="/yooome/golang/issues"><i class='iconfont icon-task'></i>
Issues
<span class='ui mini circular label'>
7
</span>
</a><a class="item " href="/yooome/golang/pulls"><i class='iconfont icon-pull-request'></i>
Pull Requests
<span class='ui mini circular label'>
2
</span>
</a><a class="item " href="/yooome/golang/wikis"><i class='iconfont icon-wiki'></i>
Wiki
</a><a class="item  " href="/yooome/golang/graph/main"><i class='iconfont icon-statistics'></i>
Insights
</a><a class="item " href="/yooome/golang/gitee_go"><i class='iconfont icon-workflow'></i>
Pipelines
</a><div class='item'>
<div class='ui pointing top right dropdown git-project-service'>
<div>
<i class='iconfont icon-service'></i>
Service
<i class='dropdown icon'></i>
</div>
<div class='menu' style='display:none'>
<a class="item" href="/yooome/golang/pages"><img src="/static/images/logo-en.svg" alt="Logo en" />
<div class='item-title'>
Gitee Pages
</div>
</a><a class="item" href="/yooome/golang/quality_analyses?platform=sonar_qube"><img src="https://cn-assets.gitee.com/assets/sonar_mini-5e1b54bb9f6c951d97fb778ef623afea.png" alt="Sonar mini" />
<div class='item-title'>
Quality Analysis
</div>
</a><a class="item" target="_blank" href="https://gitee.com/help/articles/4193"><img src="https://cn-assets.gitee.com/assets/jenkins_for_gitee-554ec65c490d0f1f18de632c48acc4e7.png" alt="Jenkins for gitee" />
<div class='item-title'>
Jenkins for Gitee
</div>
</a><a class="item" target="_blank" href="https://gitee.com/help/articles/4318"><img src="https://cn-assets.gitee.com/assets/cloudbase-1197b95ea3398aff1df7fe17c65a6d42.png?20200925" alt="Cloudbase" />
<div class='item-title'>
Tencent CloudBase
</div>
</a><a class="item" target="_blank" href="https://gitee.com/help/articles/4330"><img src="https://cn-assets.gitee.com/assets/cloud_serverless-686cf926ced5d6d2f1d6e606d270b81e.png" alt="Cloud serverless" />
<div class='item-title'>
Tencent Cloud Serverless
</div>
</a><a class="item" href="/yooome/golang/open_sca"><img src="https://cn-assets.gitee.com/assets/open_sca/logo-9049ced662b2f9936b8001e6f9cc4952.png" alt="Logo" />
<div class='item-title'>
悬镜安全
</div>
</a><a class="item" target="_blank" href="https://help.gitee.com/devops/connect/Aliyun-SAE"><img src="https://cn-assets.gitee.com/assets/SAE-f3aa9366a1e2b7fff4747402eb8f10c3.png" alt="Sae" />
<div class='item-title'>
Aliyun SAE
</div>
</a><a class="item" id="update-codeblitz-link" target="_blank" href="https://codeblitz.cloud.alipay.com/gitee/yooome/golang/tree/main/21-k8s详细教程/Kubernetes详细教程.md"><img style="width:100px;margin-top:4px" src="https://cn-assets.gitee.com/assets/Codeblitz-8824e38875a106e16e29ff57ec977b08.png" alt="Codeblitz" />
<div class='item-title'>
Codeblitz
</div>
</a><a class="item" id="update-codeblitz-link" target="_blank" href="/yooome/golang/sbom"><img style="width:30px;margin-top:4px" src="https://cn-assets.gitee.com/assets/SBOM-36dbd3141411c5c1e9095e8d1d21baf0.png" alt="Sbom" />
<div class='item-title'>
SBOM
</div>
</a><button class='ui orange basic button quit-button' id='quiting-button'>
Don’t show this again
</button>
</div>
</div>
</div>
</div>
</div>
</div>
<script>
  $('.git-project-nav .ui.dropdown').dropdown({ action: 'nothing' });
  var gitee_reward_config = JSON.parse(localStorage.getItem('gitee_reward_config') || null) || false
  var $settingText = $('.setting-text')
  // 如果没有访问过
  if(!gitee_reward_config) $settingText.addClass('red-dot')
  $('.git-project-service').dropdown({
    on: 'click',
    action: 'nothing',
    onShow: function () {
      const branch = 'main'
      let newUrl = `https://codeblitz.cloud.alipay.com/gitee/yooome/golang/tree/`
      const url = decodeURIComponent(window.location.pathname);
      const startIndex = url.indexOf('main');
      if (startIndex !== -1) {
        newUrl = newUrl + url.substring(startIndex); // 从分支名开始截取
      }else{
        newUrl = newUrl + branch
      }
      const linkElement = document.getElementById("update-codeblitz-link");
      linkElement.setAttribute("href", newUrl);
    },
  })
</script>
<style>
  .git-project-nav i.checkmark.icon {
    color: green;
  }
  #quiting-button {
    display: none;
  }
  
  .git-project-nav .dropdown .menu.hidden:after {
    visibility: hidden !important;
  }
</style>
<script>
  isSignIn = false
  isClickGuide = false
  $('#git-versions.dropdown').dropdown();
  $.ajax({
    url:"/yooome/golang/access/add_access_log",
    type:"GET"
  });
  $('#quiting-button').on('click',function() {
    $('.git-project-service').click();
    if (isSignIn) {
      $.post("/projects/set_service_guide")
    }
    $.cookie("Serve_State", true, { expires: 3650, path: '/'})
    $('#quiting-button').hide();
  });
  if (!(isClickGuide || $.cookie("Serve_State") == 'true')) {
    $('.git-project-service').click()
    $('#quiting-button').show()
  }
</script>

</div>
<div class='ui container'>
<div class='register-guide'>
<div class='register-container'>
<div class='regist'>
Create your Gitee Account
</div>
<div class='description'>
Explore and code with more than 13.5 million developers，Free private repositories ！：）
</div>
<a class="ui orange button free-registion" href="/signup?from=project-guide">Sign up</a>
<div class='login'>
Already have an account?
<a href="/login?from=project-guide">Sign in</a>
</div>
</div>
</div>

<script defer='defer' src='/static/javascripts/file-icons.js'></script>
<div class='git-project-content-wrapper'>

<div class='ui grid blob-ddd' id='project-wrapper'>
<div class='project-left-side-contaner wide column left-side' id='project-left-side-contaner'>
<link href='/webpacks/osc-element-ui-theme/index.css' rel='stylesheet' type='text/css'>
<div class='left-side-container' style='height: 100%'>
<div class='d-flex-between'>
<div class='d-align-center' id='left-head_root_file'>
<div class='file-iconify-item' onclick="$('.project-left-side-contaner').hide();$('#file-iconify-wrapper').removeClass('hide').addClass('d-align-center')">
<span class='iconify' data-icon='gitee:sidebar-expand' style='font-size: 16px;'></span>
</div>
<span class='text-bold'>文件</span>
</div>
<div class='ml-1' id='left-head_root_actions' style='flex: 1'>
<div class='ui horizontal list repo-action-list d-flex d-align-center repo-action-list-right'>
<div class='item search-box-container'>
<div class='ui icon input search-input' id='search-box'>
<input class='search-file-name' maxlength='40' placeholder='Search' type='text'>
</div>
<a class='d-flex d-align-center head-search-file-btn' id='search-file-btn'>
<span class='iconify' data-icon='gitee:search' style='font-size: 16px;color:#979CAC;margin-right:10px'></span>
</a>
<div class='filter-file-container' style='display: none;'></div>
</div>
<script>
  (function() {
    const $dropdown = $('#git-tree-file[data-id="project_tree"]');
    const dropdownEl = $dropdown[0];
    const $plusBox = $dropdown.closest('.plus-box');
    const dropdownAppendToBody = false;
    let allowHide = true;
  
    if (dropdownAppendToBody) {
      document.body.addEventListener('click', function(e) {
        allowHide = true;
        let current = e.target;
        while (current !== null) {
          if (current === dropdownEl) {
            allowHide = false;
            break;
          }
          current = current.parentElement;
        }
        if (allowHide) $dropdown.dropdown('hide');
      }, true);
    }
  
    $dropdown.dropdown({
      action: 'hide',
      onHide: function () {
        $plusBox.removeClass('click-active');
  
        return allowHide;
      },
      onShow: function () {
        $plusBox.addClass('click-active');
  
        if (!dropdownAppendToBody) return;
        const $wrapper = this.$menuWrapper || $('<div class="ui top dropdown active visible"></div>');
        const offset = $(this).offset();
        $wrapper.css({
          position: 'absolute',
          top: offset.top,
          left: offset.left,
          marginTop: '1rem',
          zIndex: 1000
        });
  
        if (this.loaded) return;
  
        // destroy prev dropdown
        document.querySelectorAll('.ui.dropdown[data-prev-dropdown]').forEach(function(el) {
          el.parentNode.removeChild(el);
        });
        const $menu = $(this).find('.menu');
        $menu.css({
          display: 'block',
          border: '1px solid rgba(34,36,38,0.15)',
          borderRadius: '4px',
          boxShadow: '0px 2px 3px 0px rgba(34, 36, 38, 0.15)'
        });
        // 移动到 body
        $wrapper.append($menu);
        $wrapper.appendTo('body');
        $wrapper.attr('data-prev-dropdown', '');
        this.$menuWrapper = $wrapper;
        this.loaded = true;
      }
    });
  })();
  
  $('#git-project-root-actions #git-tree-file').on('click', function() {
    $('#git-project-root-actions .plus-box').addClass('click-active')
    $('#git-project-root-actions .repo-dropdown-box').addClass('transition visible')
  })
  
  $('.disabled-upload-readonly').popup({
    content: "Readonly directory does not allow uploading files",
    className: {
      popup: 'ui popup',
    },
    position: 'bottom center',
  })
  $('.disabled-create-folder').popup({
    content: "Readonly directory does not allow directory creation",
    className: {
      popup: 'ui popup',
    },
    position: 'bottom center',
  })
  $('.disabled-create-file').popup({
    content: "Readonly directory does not allow files creation",
    className: {
      popup: 'ui popup',
    },
    position: 'bottom center',
  })
  $('.disabled-create-submodule').popup({
    content: "Readonly directory does not allow submodule creation",
    className: {
      popup: 'ui popup',
    },
    position: 'bottom center',
  })
  $('.disabled-upload-readonly, .disabled-create-folder, .disabled-create-file, .disabled-create-submodule').click(function() {
    return false
  })
</script>
<style>
  .disabled-upload-readonly, .disabled-create-file, .disabled-create-folder, .disabled-create-submodule {
    background-color: #dcddde !important;
    color: rgba(0, 0, 0, 0.4) !important;
    opacity: 0.3 !important;
    background-image: none !important;
    -webkit-box-shadow: none !important;
            box-shadow: none !important; }
</style>

</div>
<script>
  $('.webIDE-box').popup()
</script>
<script src="https://cn-assets.gitee.com/assets/file_search/app-21e8df8af6aa09b8995390509269205b.js"></script>
<style>
  .filter-file-container-hide {
    display: none !important; }
</style>

</div>
</div>
<div class='left-project-branch-item git-project-branch-item'>
<input type="hidden" name="path" id="path" value="21-k8s详细教程/Kubernetes详细教程.md" />
<div class='ui top left pointing dropdown gradient button dropdown-has-tabs' id='git-project-branch'>
<input type="hidden" name="ref" id="ref" value="main" />
<div class='default text'>
main
</div>
<i class='dropdown icon'></i>
<div class='menu'>
<div class='ui left icon input'>
<span class='dropdown-search-icon iconify' data-icon='gitee:search' style='font-size: 14px;'></span>
<input class='search-branch' placeholder='Search branch' type='text'>
</div>
<div class='tab-menu project-branch-tab-menu d-flex'>
<div class='tab-menu-item' data-placeholder='Search branches' data-tab='branches'>
Branches (1)
</div>
<div class='d-align-center' style='flex:1;justify-content:end;'>
<div class='tab-menu-action' data-tab='branches'>
<a class="ui link button" href="/yooome/golang/branches">Manage</a>
</div>
<div class='tab-menu-action' data-tab='tags'>
<a class="ui link button" href="/yooome/golang/tags">Manage</a>
</div>
</div>
</div>
<div class='tab scrolling menu' data-tab='branches' id='branches_panel'>
<div data-value="main" class="item" title="main"><span class="iconify" data-icon="gitee:branch" style="font-size: 13px;margin-right:4px; color:#8C92A4"></span> <span>main</span></div>
</div>
</div>
</div>
<style>
  .iconfont.icon-shieldlock {
    color: #8c92a4;
  }
  .dropdown-search-icon {
    position: absolute;
    top: 8px;
    left: 11px;
  }
</style>
<style>
  #git-project-branch .project-branch-tab-menu, .project-branch-item .project-branch-tab-menu {
    padding-left: 0px !important;
    padding-right: 0px !important;
    margin: 0 11px !important;
    border-bottom: 1px solid #dfe3e9 !important; }
  #git-project-branch .ui.dropdown .menu, .project-branch-item .ui.dropdown .menu {
    width: 360px !important; }
    #git-project-branch .ui.dropdown .menu .item, .project-branch-item .ui.dropdown .menu .item {
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap; }
  #git-project-branch .tab-menu-actions, .project-branch-item .tab-menu-actions {
    position: absolute;
    right: 0px !important;
    bottom: 0.357em; }
  #git-project-branch .tab-menu-action, .project-branch-item .tab-menu-action {
    position: relative !important;
    right: 0px !important;
    bottom: 0px !important; }
  #git-project-branch .menu::after, .project-branch-item .menu::after {
    display: none !important; }
</style>
<script>
  var $branchesDropdown = $('#branches_panel');
  var $tagsDropdown = $('#tags_panel');
  var $searchNameInput = $('.search-branch');
  var concurrentRequestLock = false;
  var filterXSS = window.filterXSS;
  var search_text = "";
  var branch_page_number = 1;
  var branch_total_pager = Math.ceil(1 / 20) || 1
  
  var flag_is_loading = false;
  var flag_page_number = 1;
  var flag_total_pager = Math.ceil(0 / 20) || 1
  
  $branchesDropdown.scroll(function() {
    var branchesPanel = document.getElementById('branches_panel');
    var numOfBranches = $branchesDropdown.children().length;
    if (branchesPanel.clientHeight + branchesPanel.scrollTop + 37 > branchesPanel.scrollHeight && numOfBranches < 1) {
      debounceLoadMoreBranches.call();
    }
  });
  function resetFlagVal() {
    flag_is_loading = false;
    flag_page_number = 1;
    flag_total_pager = 1;
  
    concurrentRequestLock = false
    search_text = "";
    branch_page_number = 1;
    branch_total_pager = 1
  }
  $searchNameInput.on('input', window.globalUtils.debouce(function (e) {
    resetFlagVal()
    var $currentTab = $('.tab-menu-action.active');
    var numOfBranches = $branchesDropdown.children().length;
    var searchWord = $searchNameInput.val().trim();
    search_text = searchWord
    if($currentTab.data('tab') === 'branches') {
      if (searchWord !== "") {
        loadData(searchWord,1);
      } else {
        loadData();
      }
    }
    var numOfTags = $tagsDropdown.children().length;
    if($currentTab.data('tab') === 'tags') {
      if (searchWord !== "") {
        fetchTags(searchWord,1);
      } else {
        fetchTags();
      }
    }
  }, 500));
  
  function toggleNoResultView($popPanel) {
    let no_data_html= `<div class='mt-1 mb-1 d-flex-center'> <span>暂无数据</span> </div>`
    $popPanel.append(no_data_html)
  }
  var debounceLoadMoreBranches = window.globalUtils.debouce(function () {
    if (concurrentRequestLock) return;
    branch_page_number += 1;
    if (branch_page_number > branch_total_pager) return;
    loadData(search_text, branch_page_number);
  }, 350);
  
  function loadData(search, page) {
    if (concurrentRequestLock) { return; }
    concurrentRequestLock = true;
  
    var searchParams = search || "";
    var pageParams = page || 1;
    $.ajax({
      url: "/" + gon.user_project + "/branches/names.json",
      type: 'GET',
      data: {
        search: searchParams,
        page: pageParams,
      },
      dataType: 'json',
      success: function (data) {
        branch_total_pager = data.total_pages;
        var html = '';
  
        if (pageParams === 1) {
          $branchesDropdown.empty();
        }
        data.branches.forEach(function (branch) {
          var protectRule = '';
          var branchName = filterXSS(branch.name);
          var icon = 'gitee:branch'
          if(branch.branch_type.value === 1) {
            var rule = filterXSS(branch.protection_rule.wildcard);
            protectRule = `<i
                class="iconfont icon-shieldlock protected-branch-popup"
                data-title="受保护分支"
                data-content='保护规则： ${rule}'
              >
              </i>`
            icon ='gitee:pen-lock'
          }else if(branch.branch_type.value === 2) {
            icon ='gitee:pen-ban'
          }
          var branchIcon = `<span class="iconify" data-icon=${icon} style="font-size: 13px; margin-right:4px; color:#8C92A4"></span>`
          html += `<div data-value='${branchName}' class="item">
                    ${branchIcon} 
                    <span>${branchName}</span> ${protectRule}
                    </div>`
        });
        $branchesDropdown.append(html);
        $('.protected-branch-popup').popup()
        if (pageParams === 1 && data.count === 0) {
          toggleNoResultView($branchesDropdown);
        }
      },
      complete: function () {
        concurrentRequestLock = false;
      }
    });
  }
  
  
  
  $tagsDropdown.scroll(function() {
    var tagsPanel = document.getElementById('tags_panel');
    var numOfTags = $tagsDropdown.children().length;
    if (tagsPanel.clientHeight + tagsPanel.scrollTop + 37 > tagsPanel.scrollHeight && numOfTags < 0) {
      debounceLoadMore.call();
    }
  });
  var debounceLoadMore = window.globalUtils.debouce(function () {
    if (flag_is_loading) return;
    flag_page_number += 1;
    if (flag_page_number > flag_total_pager) return;
    fetchTags(search_text, flag_page_number);
  }, 350);
  
  function fetchTags(search, page) {
    var searchParams = search || "";
    var pageParams = page || 1;
  
    if (flag_is_loading) return;
    flag_is_loading = true;
  
    $.ajax({
      url: "/" + gon.user_project + "/tags/names.json",
      data: {
        search: searchParams,
        page: pageParams,
      },
      type: "GET",
      xhrFields: {
        withCredentials: true,
      },
      success: function (data) {
        flag_total_pager = data.total_pages;
        if (pageParams === 1) {
          $tagsDropdown.html('');
        }
        data.tags.forEach((tag) => {
          const itemDiv = document.createElement('div');
          itemDiv.classList.add('item');
          itemDiv.setAttribute('data-value', tag.name);
          itemDiv.innerText = window.filterXSS(tag.name);
          $tagsDropdown.append(itemDiv)
        });
        if (pageParams === 1 && data.count === 0) {
          toggleNoResultView($tagsDropdown);
        }
      },
      error: function () {
      },
      complete: function () {
        flag_is_loading = false;
      },
    });
  }
  $('.project-branch-tab-menu').on('click','.tab-menu-item', function (e) {
    var $currentTab = $(this).data('tab')
    if($currentTab === 'branches') {
      $searchNameInput.val('')
      search_text = '';
      loadData()
    }
    if($currentTab === 'tags') {
      $searchNameInput.val('')
      search_text = '';
      fetchTags();
    }
  })
</script>

<script>
  $(function () {
    var curNode = $('.git-project-branch-item')
    if (true ){
      curNode = $('.left-project-branch-item')
    }else {
      curNode = $('.git-project-branch-item')
    }
    Gitee.initTabsInDropdown(curNode.find('#git-project-branch').dropdown({
      fullTextSearch: true,
      selectOnKeydown: false,
      direction: 'downward',
      action: function (text,value,el) {
        var oItemOrInitObject = el[0] || el
        var isNotSelect = oItemOrInitObject.dataset.tab && oItemOrInitObject.dataset.tab === 'branches'
        if(isNotSelect){
          console.warn("You didn't choose a branch")
          return
        }
        var path = $('#path').val();
        var href = ['/yooome/golang/tree', encodeURIComponent(value), path].join('/');
        window.location.href = href;
        return true
      },
      onNoResults: function (searchTerm) {
        //未找到结果
        return true
      },
    }));
    $('.protected-branch-popup').popup()
  })
</script>

</div>
<div data-init-path='21-k8s详细教程/Kubernetes详细教程.md' data-repo-path='yooome/golang' id='project-tree-container'></div>
</div>
<style>
  .left-side-container {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column; }
    .left-side-container .file-iconify-item {
      display: -webkit-box;
      display: -ms-flexbox;
      display: flex;
      padding: 8px;
      border-radius: 4px;
      margin-right: 8px;
      width: 32px;
      height: 32px;
      text-align: center; }
      .left-side-container .file-iconify-item:hover {
        background-color: #f5f7fa; }
</style>
<script>
  if (!false && window.Gitee.setFullscreen){
    window.Gitee.setFullscreen(true);
  }else {
    window.Gitee.setFullscreen(false);
  }
</script>
<script src="https://cn-assets.gitee.com/webpacks/vendors_lib-7ff466a6da368d391eda.js" defer="defer"></script>
<script src="https://cn-assets.gitee.com/webpacks/project_tree-ba13b418949b59a59ed6.bundle.js" defer="defer"></script>

</div>
<div class='sixteen wide column right-wrapper' id='sixteen'>
<div class='git-project-content' id='git-project-content'>
<div class='row'>
<div class='git-project-desc-wrapper'>
<script>
  $('.git-project-desc-wrapper .ui.dropdown').dropdown();
  if (false) {
    gon.project_new_blob_path = "/yooome/golang/new/main/21-k8s%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B/Kubernetes%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B.md"
    bindShowModal({
      el: $('.no-license .project-license__create'),
      complete: function(data, modal) {
        if (!data.haveNoChoice && !data.data) {
          Flash.show('Please select an open source license')
        } else {
          location.href = gon.project_new_blob_path + '?license=' + data.data
        }
      },
      skip: function () {
        location.href = gon.project_new_blob_path + '?license'
      }
    });
  }
  
  $(".project-admin-action-box .reject").click(function() {
    var reason = $('[name=review-reject-reason]').val();
    if (!reason) {
      Flash.error('请选择不通过理由')
      return
    }
    $.ajax({
      type: 'POST',
      url: "/admin/shumei_content/shumei_check/reject_project_public",
      data: {
        reason: reason,
        status: 'rejected',
        project_id: 14603335
      },
      success: function(result){
        if(result.status == 'success'){
          window.location.reload();
        }else{
          Flash.error(result.message)
        }
      }
    })
  })
  
  $(".project-admin-action-box .approve").click(function(){
  
    $.ajax({
      type: 'POST',
      url: "/admin/shumei_content/shumei_check/reject_project_public",
      data: {
        status: 'approved',
        project_id: 14603335
      },
      success: function(result){
        if(result.status == 'success'){
          window.location.reload();
        }else{
          Flash.error(result.message)
        }
      }
    })
  })
  
  $(".project-admin-action-box .waiting").click(function(){
  
    $.ajax({
      type: 'POST',
      url: "/admin/shumei_content/shumei_check/reject_project_public",
      data: {
        status: 'waiting',
        project_id: 14603335
      },
      success: function(result){
        if(result.status == 'success'){
          window.location.reload();
        }else{
          Flash.error(result.message)
        }
      }
    })
  })
  
  $('i.help.circle.icon').popup({
    popup: '.no-license .ui.popup',
    position: 'right center'
  });
  
  $('#remove-no-license-message').on('click', function() {
    $.cookie("skip_repo_no_license_message_14603335", 'hide', { expires: 365 });
    $('#user-no-license-message').hide();
    return;
  });
</script>
</div>

</div>
<div class='git-project-bread' id='git-project-bread'>
<div class='ui horizontal list mr-1' id='git-branch-dropdown' style='display: none;'>
<div class='item git-project-branch-item'>
<input type="hidden" name="path" id="path" value="21-k8s详细教程/Kubernetes详细教程.md" />
<div class='ui top left pointing dropdown gradient button dropdown-has-tabs' id='git-project-branch'>
<input type="hidden" name="ref" id="ref" value="main" />
<div class='default text'>
main
</div>
<i class='dropdown icon'></i>
<div class='menu'>
<div class='ui left icon input'>
<span class='dropdown-search-icon iconify' data-icon='gitee:search' style='font-size: 14px;'></span>
<input class='search-branch' placeholder='Search branch' type='text'>
</div>
<div class='tab-menu project-branch-tab-menu d-flex'>
<div class='tab-menu-item' data-placeholder='Search branches' data-tab='branches'>
Branches (1)
</div>
<div class='d-align-center' style='flex:1;justify-content:end;'>
<div class='tab-menu-action' data-tab='branches'>
<a class="ui link button" href="/yooome/golang/branches">Manage</a>
</div>
<div class='tab-menu-action' data-tab='tags'>
<a class="ui link button" href="/yooome/golang/tags">Manage</a>
</div>
</div>
</div>
<div class='tab scrolling menu' data-tab='branches' id='branches_panel'>
<div data-value="main" class="item" title="main"><span class="iconify" data-icon="gitee:branch" style="font-size: 13px;margin-right:4px; color:#8C92A4"></span> <span>main</span></div>
</div>
</div>
</div>
<style>
  .iconfont.icon-shieldlock {
    color: #8c92a4;
  }
  .dropdown-search-icon {
    position: absolute;
    top: 8px;
    left: 11px;
  }
</style>
<style>
  #git-project-branch .project-branch-tab-menu, .project-branch-item .project-branch-tab-menu {
    padding-left: 0px !important;
    padding-right: 0px !important;
    margin: 0 11px !important;
    border-bottom: 1px solid #dfe3e9 !important; }
  #git-project-branch .ui.dropdown .menu, .project-branch-item .ui.dropdown .menu {
    width: 360px !important; }
    #git-project-branch .ui.dropdown .menu .item, .project-branch-item .ui.dropdown .menu .item {
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap; }
  #git-project-branch .tab-menu-actions, .project-branch-item .tab-menu-actions {
    position: absolute;
    right: 0px !important;
    bottom: 0.357em; }
  #git-project-branch .tab-menu-action, .project-branch-item .tab-menu-action {
    position: relative !important;
    right: 0px !important;
    bottom: 0px !important; }
  #git-project-branch .menu::after, .project-branch-item .menu::after {
    display: none !important; }
</style>
<script>
  var $branchesDropdown = $('#branches_panel');
  var $tagsDropdown = $('#tags_panel');
  var $searchNameInput = $('.search-branch');
  var concurrentRequestLock = false;
  var filterXSS = window.filterXSS;
  var search_text = "";
  var branch_page_number = 1;
  var branch_total_pager = Math.ceil(1 / 20) || 1
  
  var flag_is_loading = false;
  var flag_page_number = 1;
  var flag_total_pager = Math.ceil(0 / 20) || 1
  
  $branchesDropdown.scroll(function() {
    var branchesPanel = document.getElementById('branches_panel');
    var numOfBranches = $branchesDropdown.children().length;
    if (branchesPanel.clientHeight + branchesPanel.scrollTop + 37 > branchesPanel.scrollHeight && numOfBranches < 1) {
      debounceLoadMoreBranches.call();
    }
  });
  function resetFlagVal() {
    flag_is_loading = false;
    flag_page_number = 1;
    flag_total_pager = 1;
  
    concurrentRequestLock = false
    search_text = "";
    branch_page_number = 1;
    branch_total_pager = 1
  }
  $searchNameInput.on('input', window.globalUtils.debouce(function (e) {
    resetFlagVal()
    var $currentTab = $('.tab-menu-action.active');
    var numOfBranches = $branchesDropdown.children().length;
    var searchWord = $searchNameInput.val().trim();
    search_text = searchWord
    if($currentTab.data('tab') === 'branches') {
      if (searchWord !== "") {
        loadData(searchWord,1);
      } else {
        loadData();
      }
    }
    var numOfTags = $tagsDropdown.children().length;
    if($currentTab.data('tab') === 'tags') {
      if (searchWord !== "") {
        fetchTags(searchWord,1);
      } else {
        fetchTags();
      }
    }
  }, 500));
  
  function toggleNoResultView($popPanel) {
    let no_data_html= `<div class='mt-1 mb-1 d-flex-center'> <span>暂无数据</span> </div>`
    $popPanel.append(no_data_html)
  }
  var debounceLoadMoreBranches = window.globalUtils.debouce(function () {
    if (concurrentRequestLock) return;
    branch_page_number += 1;
    if (branch_page_number > branch_total_pager) return;
    loadData(search_text, branch_page_number);
  }, 350);
  
  function loadData(search, page) {
    if (concurrentRequestLock) { return; }
    concurrentRequestLock = true;
  
    var searchParams = search || "";
    var pageParams = page || 1;
    $.ajax({
      url: "/" + gon.user_project + "/branches/names.json",
      type: 'GET',
      data: {
        search: searchParams,
        page: pageParams,
      },
      dataType: 'json',
      success: function (data) {
        branch_total_pager = data.total_pages;
        var html = '';
  
        if (pageParams === 1) {
          $branchesDropdown.empty();
        }
        data.branches.forEach(function (branch) {
          var protectRule = '';
          var branchName = filterXSS(branch.name);
          var icon = 'gitee:branch'
          if(branch.branch_type.value === 1) {
            var rule = filterXSS(branch.protection_rule.wildcard);
            protectRule = `<i
                class="iconfont icon-shieldlock protected-branch-popup"
                data-title="受保护分支"
                data-content='保护规则： ${rule}'
              >
              </i>`
            icon ='gitee:pen-lock'
          }else if(branch.branch_type.value === 2) {
            icon ='gitee:pen-ban'
          }
          var branchIcon = `<span class="iconify" data-icon=${icon} style="font-size: 13px; margin-right:4px; color:#8C92A4"></span>`
          html += `<div data-value='${branchName}' class="item">
                    ${branchIcon} 
                    <span>${branchName}</span> ${protectRule}
                    </div>`
        });
        $branchesDropdown.append(html);
        $('.protected-branch-popup').popup()
        if (pageParams === 1 && data.count === 0) {
          toggleNoResultView($branchesDropdown);
        }
      },
      complete: function () {
        concurrentRequestLock = false;
      }
    });
  }
  
  
  
  $tagsDropdown.scroll(function() {
    var tagsPanel = document.getElementById('tags_panel');
    var numOfTags = $tagsDropdown.children().length;
    if (tagsPanel.clientHeight + tagsPanel.scrollTop + 37 > tagsPanel.scrollHeight && numOfTags < 0) {
      debounceLoadMore.call();
    }
  });
  var debounceLoadMore = window.globalUtils.debouce(function () {
    if (flag_is_loading) return;
    flag_page_number += 1;
    if (flag_page_number > flag_total_pager) return;
    fetchTags(search_text, flag_page_number);
  }, 350);
  
  function fetchTags(search, page) {
    var searchParams = search || "";
    var pageParams = page || 1;
  
    if (flag_is_loading) return;
    flag_is_loading = true;
  
    $.ajax({
      url: "/" + gon.user_project + "/tags/names.json",
      data: {
        search: searchParams,
        page: pageParams,
      },
      type: "GET",
      xhrFields: {
        withCredentials: true,
      },
      success: function (data) {
        flag_total_pager = data.total_pages;
        if (pageParams === 1) {
          $tagsDropdown.html('');
        }
        data.tags.forEach((tag) => {
          const itemDiv = document.createElement('div');
          itemDiv.classList.add('item');
          itemDiv.setAttribute('data-value', tag.name);
          itemDiv.innerText = window.filterXSS(tag.name);
          $tagsDropdown.append(itemDiv)
        });
        if (pageParams === 1 && data.count === 0) {
          toggleNoResultView($tagsDropdown);
        }
      },
      error: function () {
      },
      complete: function () {
        flag_is_loading = false;
      },
    });
  }
  $('.project-branch-tab-menu').on('click','.tab-menu-item', function (e) {
    var $currentTab = $(this).data('tab')
    if($currentTab === 'branches') {
      $searchNameInput.val('')
      search_text = '';
      loadData()
    }
    if($currentTab === 'tags') {
      $searchNameInput.val('')
      search_text = '';
      fetchTags();
    }
  })
</script>

<script>
  $(function () {
    var curNode = $('.git-project-branch-item')
    if (true ){
      curNode = $('.left-project-branch-item')
    }else {
      curNode = $('.git-project-branch-item')
    }
    Gitee.initTabsInDropdown(curNode.find('#git-project-branch').dropdown({
      fullTextSearch: true,
      selectOnKeydown: false,
      direction: 'downward',
      action: function (text,value,el) {
        var oItemOrInitObject = el[0] || el
        var isNotSelect = oItemOrInitObject.dataset.tab && oItemOrInitObject.dataset.tab === 'branches'
        if(isNotSelect){
          console.warn("You didn't choose a branch")
          return
        }
        var path = $('#path').val();
        var href = ['/yooome/golang/tree', encodeURIComponent(value), path].join('/');
        window.location.href = href;
        return true
      },
      onNoResults: function (searchTerm) {
        //未找到结果
        return true
      },
    }));
    $('.protected-branch-popup').popup()
  })
</script>

</div>
</div>
<div class='git-project-right-actions pull-right'>
<div class='ui basic orange button' id='btn-dl-or-clone'>
Clone or Download
<i class='dropdown icon'></i>
</div>
<div class='ui small modal' id='git-project-download-panel'>
<i class='iconfont icon-close close'></i>
<div class='header'>
Clone/Download
</div>
<div class='content'>
<div class='ui secondary pointing menu mb-2 menu-container'>
<a class='item active' data-text='' data-type='http' data-url='https://gitee.com/yooome/golang.git'>HTTPS</a>
<a class='item' data-text='' data-type='ssh' data-url='git@gitee.com:yooome/golang.git'>SSH</a>
<a class='item' data-text="The repository has forbidden SVN access. if you need it, please visit: &lt;a target='_blank' href=/yooome/golang/settings#function&gt;Repository security settings&lt;/a&gt;" data-type='svn' data-url=''>SVN</a>
<a class='item' data-text="The repository has forbidden SVN access. if you need it, please visit: &lt;a target='_blank' href=/yooome/golang/settings#function&gt;Repository security settings&lt;/a&gt;" data-type='svn_ssh' data-url=''>SVN+SSH</a>
<a class="ui basic orange button button-box unlogin-download-btn" href="javascript:void(0);"><i class='icon download'></i>
Download ZIP
</a><div class='ui custom popup popup'>
<div class='popup-container actions'>
<div class='content'>
This operation requires login to the code cloud account. Please log in before operating.
</div>
<a class="ui orange button ok icon" href="/login?from=download_repository_zip">Go to login
</a><a class="ui blank button cancel" href="/signup?from=download_repository_zip">No account. Register
</a></div>
</div>
</div>
<div class='ui fluid right labeled small input download-url-panel mb-2'>
<input type="text" name="project_url_clone" id="project_url_clone" value="https://gitee.com/yooome/golang.git" onclick="focus();select()" readonly="readonly" />
<div class='ui basic label copy-icon-box'>
<i class='icon iconfont icon-clone mr-0 btn-copy-clone' data-clipboard-target='#project_url_clone' id='btn-copy-project_clone_url1'></i>
</div>
</div>
<div class='tip-box mb-2'>
Prompt
</div>
<div class='mb-1 clone-url-title'>
To download the code, please copy the following command and execute it in the terminal
</div>
<div class='ui fluid right labeled small input download-url-panel mb-2'>
<input type="text" name="project_clone_url" id="project_clone_url" value="https://gitee.com/yooome/golang.git" onclick="focus();select()" readonly="readonly" />
<div class='ui basic label copy-icon-box'>
<i class='icon iconfont icon-clone mr-0 btn-copy-clone' data-clipboard-target='#project_clone_url' id='btn-copy-project_clone_url'></i>
</div>
</div>
<div class='ui fluid right labeled warning-text forbid-warning-text'>

</div>
<div class='http-ssh-item mb-2'>
<div>
To ensure that your submitted code identity is correctly recognized by Gitee, please execute the following command.
</div>
<div class='textarea-box mt-2'>
<textarea class='textarea-content-box' id='global-config-clone' readonly>git config --global user.name userName &#10git config --global user.email userEmail</textarea>
<i class='icon iconfont icon-clone mr-2 btn-copy-clone text-dark' data-clipboard-target='#global-config-clone' id='btn-copy-global-config'></i>
</div>
</div>
<div class='ssh-item item-panel-box'>
<div class='mb-2'>
When using the SSH protocol for the first time to clone or push code, follow the prompts below to complete the SSH configuration.
</div>
<div class='mb-1'>
<span>1</span>
Generate RSA keys.
</div>
<div class='ui fluid right labeled small input mb-2'>
<input type="text" name="ssh_keygen_clone" id="ssh_keygen_clone" value="ssh-keygen -t rsa" onclick="focus();select()" readonly="readonly" />
<div class='ui basic label copy-icon-box'>
<i class='icon iconfont icon-clone mr-0 btn-copy-clone' data-clipboard-target='#ssh_keygen_clone' id='btn-copy-ssh_keygen'></i>
</div>
</div>
<div class='mb-1'>
<span>2</span>
Obtain the content of the RSA public key and configure it in <a href='/profile/sshkeys' target="_blank">SSH Public Keys</a>
</div>
<div class='ui fluid right labeled small input mb-2'>
<input type="text" name="id_rsa_clone" id="id_rsa_clone" value="cat ~/.ssh/id_rsa.pub" onclick="focus();select()" readonly="readonly" />
<div class='ui basic label copy-icon-box'>
<i class='icon iconfont icon-clone mr-0 btn-copy-clone' data-clipboard-target='#id_rsa_clone' id='btn-copy-d_rsa'></i>
</div>
</div>
</div>
<div class='svn-item item-panel-box'>
<div class='mb-1 mt-2'>
To use SVN on Gitee, please visit <a href='https://help.gitee.com/enterprise/code-manage/%E4%BB%A3%E7%A0%81%E6%89%98%E7%AE%A1/%E4%BB%A3%E7%A0%81%E4%BB%93%E5%BA%93/Gitee%20SVN%E6%94%AF%E6%8C%81' target="_blank">the usage guide</a>
</div>
</div>
<div class='http-item item-panel-box'>
<div class='mb-2 mt-2'>
When using the HTTPS protocol, the command line will prompt for account and password verification as follows. For security reasons, Gitee recommends <a href='/profile/personal_access_tokens' target="_blank">configure and use personal access tokens</a> instead of login passwords for cloning, pushing, and other operations.
</div>
<div>Username for 'https://gitee.com': userName</div>
<div class='mb-1'>
<span>Password for 'https://userName@gitee.com':</span>
<span>#</span>
<span>
Private Token
</span>
</div>
</div>
</div>
</div>
<style>
  #git-project-download-panel {
    top: 90px !important; }
    #git-project-download-panel input {
      color: #40485b !important; }
    #git-project-download-panel .textarea-box {
      width: 100%;
      height: 60px;
      color: #9d9d9d;
      border-radius: 2px;
      background-color: #F5F5F5 !important;
      display: -webkit-box;
      display: -ms-flexbox;
      display: flex;
      -webkit-box-align: center;
          -ms-flex-align: center;
              align-items: center; }
    #git-project-download-panel .menu-container {
      font-weight: bold;
      border-color: rgba(0, 0, 0, 0.1) !important;
      border-bottom: 1px solid rgba(0, 0, 0, 0.1) !important; }
      #git-project-download-panel .menu-container .item {
        padding: 7px 12px !important; }
    #git-project-download-panel .hr-item {
      color: rgba(39, 41, 43, 0.15) !important; }
    #git-project-download-panel .textarea-content-box {
      width: 100%;
      height: 60px;
      resize: none;
      border: 0px !important;
      background-color: #F5F5F5 !important;
      color: #40485b !important; }
    #git-project-download-panel .btn-copy-clone {
      cursor: pointer;
      color: rgba(0, 0, 0, 0.87) !important; }
    #git-project-download-panel .copy-icon-box {
      background-color: #F5F5F5 !important;
      border-left: 0px !important; }
    #git-project-download-panel .button-box {
      border: 0px !important;
      float: right !important;
      padding-right: 0 !important; }
    #git-project-download-panel .tip-box {
      border-bottom: 1px solid rgba(0, 0, 0, 0.1) !important;
      padding-bottom: 4px;
      font-weight: 700; }
    #git-project-download-panel .popup-container {
      padding: 8px 12px 4px 12px;
      text-align: center;
      font-size: 14px; }
      #git-project-download-panel .popup-container .ok {
        margin: 12px auto;
        width: 25%;
        min-width: 125px;
        display: block; }
      #git-project-download-panel .popup-container .cancel {
        margin-left: 0; }
</style>
<script>
  $(function () {
    var $btnClone = $('#btn-dl-or-clone')
    var $modalDownload = $('#git-project-download-panel');
    var $input = $('#project_clone_url')
    var $inputUrl = $('#project_url_clone')
    var cloneUrlTitle= $('.clone-url-title')
  
    $('#btn-dl-or-clone').on('click', function (e) {
      e.preventDefault();
      $modalDownload.modal('show');
    })
  
    $modalDownload.find('.menu > .item').on('click', function(e) {
      var $item = $(this).addClass('active');
      $item.siblings().removeClass('active');
      var dataUrl = $item.attr('data-url');
      var cloneUrl = $item.attr('data-url');
      var dataType = $item.attr('data-type')
      var cloneToLocal = 'To download the code, please copy the following command and execute it in the terminal'
      if(dataType=='http'){
        $modalDownload.find('.http-item').show();
        $('.content > .item-panel-box:not(.http-item)').hide();
        $modalDownload.find('.http-ssh-item').show();
        cloneUrl = 'git clone '+dataUrl
      }else if(dataType=='ssh'){
        $modalDownload.find('.ssh-item').show();
        $('.content > .item-panel-box:not(.ssh-item)').hide();
        $modalDownload.find('.http-ssh-item').show();
        cloneUrl = 'git clone '+dataUrl
      }else if(dataType=='svn') {
        $('.content > .item-panel-box:not(.svn-item)').hide();
        $modalDownload.find('.svn-item').show();
        $modalDownload.find('.http-ssh-item').hide();
        cloneUrl = 'svn checkout '+dataUrl
      }else {
        $('.content > .item-panel-box:not(.svn-item)').hide();
        $modalDownload.find('.svn-item').show();
        $modalDownload.find('.http-ssh-item').hide();
        cloneUrl = 'svn checkout '+dataUrl
      }
      if (dataUrl) {
        $modalDownload.find('.download-url-panel').show();
        $input.val(cloneUrl);
        $inputUrl.val(dataUrl)
        cloneUrlTitle.show();
        $modalDownload.find('.forbid-warning-text').html('');
      } else {
        $modalDownload.find('.download-url-panel').hide();
        //$modalDownload.find('.svn-item').hide();
        cloneUrlTitle.hide();
        $modalDownload.find('.forbid-warning-text').html($item.attr('data-text') || '');
      }
      $.cookie('remote_way', $item.attr('data-type'), { expires: 365, path: '/' });
    }).filter('[data-type="' + ($.cookie('remote_way') || 'http') + '"]').trigger('click');
  
    $('.btn-copy-clone').popup({
      content: 'Copy to clipboard',
    }).on('click', function(e) {
      e.stopPropagation();
      return false;
    }).each(function(_, btnCopy) {
      var $btnCopy = $(btnCopy);
      new Clipboard(btnCopy).on('success', function() {
        $btnCopy.popup('destroy').popup({
          content: 'Copied',
          on: 'manual'
        }).popup('show');
        setTimeout(function() {
          $btnCopy.popup('destroy').popup({
            content: 'Copy to clipboard'
          });
        }, 2000);
      });
    });
    var $downloadBtn= $('.unlogin-download-btn')
    var $popupContainer = $('.popup-container')
    $downloadBtn.popup({
      popup : $('.custom.popup'),
      position   : 'bottom right',
    }).on('click', function(e) {
      $downloadBtn.popup('destroy').popup({
        popup : $('.custom.popup'),
        on: 'manual',
        position   : 'bottom right',
      }).popup('show');
      setTimeout(function() {
        $downloadBtn.popup('hide');
      }, 2000);
  
    })
  })
</script>

</div>
<div class='d-inline pull-right' id='git-project-root-actions'>
<div class='ui horizontal list repo-action-list d-flex d-align-center repo-action-list-right'>
<div class='item search-box-container'>
<div class='ui icon input search-input' id='search-box'>
<input class='search-file-name' maxlength='40' placeholder='Search' type='text'>
</div>
<a class='d-flex d-align-center head-search-file-btn' id='search-file-btn'>
<span class='iconify' data-icon='gitee:search' style='font-size: 16px;color:#979CAC;margin-right:10px'></span>
</a>
<div class='filter-file-container' style='display: none;'></div>
</div>
<script>
  (function() {
    const $dropdown = $('#git-tree-file[data-id="git-tree-file"]');
    const dropdownEl = $dropdown[0];
    const $plusBox = $dropdown.closest('.plus-box');
    const dropdownAppendToBody = false;
    let allowHide = true;
  
    if (dropdownAppendToBody) {
      document.body.addEventListener('click', function(e) {
        allowHide = true;
        let current = e.target;
        while (current !== null) {
          if (current === dropdownEl) {
            allowHide = false;
            break;
          }
          current = current.parentElement;
        }
        if (allowHide) $dropdown.dropdown('hide');
      }, true);
    }
  
    $dropdown.dropdown({
      action: 'hide',
      onHide: function () {
        $plusBox.removeClass('click-active');
  
        return allowHide;
      },
      onShow: function () {
        $plusBox.addClass('click-active');
  
        if (!dropdownAppendToBody) return;
        const $wrapper = this.$menuWrapper || $('<div class="ui top dropdown active visible"></div>');
        const offset = $(this).offset();
        $wrapper.css({
          position: 'absolute',
          top: offset.top,
          left: offset.left,
          marginTop: '1rem',
          zIndex: 1000
        });
  
        if (this.loaded) return;
  
        // destroy prev dropdown
        document.querySelectorAll('.ui.dropdown[data-prev-dropdown]').forEach(function(el) {
          el.parentNode.removeChild(el);
        });
        const $menu = $(this).find('.menu');
        $menu.css({
          display: 'block',
          border: '1px solid rgba(34,36,38,0.15)',
          borderRadius: '4px',
          boxShadow: '0px 2px 3px 0px rgba(34, 36, 38, 0.15)'
        });
        // 移动到 body
        $wrapper.append($menu);
        $wrapper.appendTo('body');
        $wrapper.attr('data-prev-dropdown', '');
        this.$menuWrapper = $wrapper;
        this.loaded = true;
      }
    });
  })();
  
  $('#git-project-root-actions #git-tree-file').on('click', function() {
    $('#git-project-root-actions .plus-box').addClass('click-active')
    $('#git-project-root-actions .repo-dropdown-box').addClass('transition visible')
  })
  
  $('.disabled-upload-readonly').popup({
    content: "Readonly directory does not allow uploading files",
    className: {
      popup: 'ui popup',
    },
    position: 'bottom center',
  })
  $('.disabled-create-folder').popup({
    content: "Readonly directory does not allow directory creation",
    className: {
      popup: 'ui popup',
    },
    position: 'bottom center',
  })
  $('.disabled-create-file').popup({
    content: "Readonly directory does not allow files creation",
    className: {
      popup: 'ui popup',
    },
    position: 'bottom center',
  })
  $('.disabled-create-submodule').popup({
    content: "Readonly directory does not allow submodule creation",
    className: {
      popup: 'ui popup',
    },
    position: 'bottom center',
  })
  $('.disabled-upload-readonly, .disabled-create-folder, .disabled-create-file, .disabled-create-submodule').click(function() {
    return false
  })
</script>
<style>
  .disabled-upload-readonly, .disabled-create-file, .disabled-create-folder, .disabled-create-submodule {
    background-color: #dcddde !important;
    color: rgba(0, 0, 0, 0.4) !important;
    opacity: 0.3 !important;
    background-image: none !important;
    -webkit-box-shadow: none !important;
            box-shadow: none !important; }
</style>

</div>
<script>
  $('.webIDE-box').popup()
</script>
<script src="https://cn-assets.gitee.com/assets/file_search/app-21e8df8af6aa09b8995390509269205b.js"></script>
<style>
  .filter-file-container-hide {
    display: none !important; }
</style>

</div>
<div class='breadcrumb_path path-breadcrumb-contrainer' id='git-project-breadcrumb'>
<div class='ui breadcrumb path project-path-breadcrumb d-flex' id='path-breadcrumb'>
<div class='mr-1 hide' id='file-iconify-wrapper'>
<div class='file-iconify-item d-align-center mr-1' onclick="$('.project-left-side-contaner').show();$('#file-iconify-wrapper').addClass('hide').removeClass('d-align-center');">
<span class='iconify' data-icon='gitee:sidebar-collapse' style='font-size: 16px;'></span>
</div>
<div class='left-project-branch-item project-branch-item' style='display: inline-block;'>
<input type="hidden" name="path" id="path" value="21-k8s详细教程/Kubernetes详细教程.md" />
<div class='ui top left pointing dropdown gradient button dropdown-has-tabs' id='git-project-branch'>
<input type="hidden" name="ref" id="ref" value="main" />
<div class='default text'>
main
</div>
<i class='dropdown icon'></i>
<div class='menu'>
<div class='ui left icon input'>
<span class='dropdown-search-icon iconify' data-icon='gitee:search' style='font-size: 14px;'></span>
<input class='search-branch' placeholder='Search branch' type='text'>
</div>
<div class='tab-menu project-branch-tab-menu d-flex'>
<div class='tab-menu-item' data-placeholder='Search branches' data-tab='branches'>
Branches (1)
</div>
<div class='d-align-center' style='flex:1;justify-content:end;'>
<div class='tab-menu-action' data-tab='branches'>
<a class="ui link button" href="/yooome/golang/branches">Manage</a>
</div>
<div class='tab-menu-action' data-tab='tags'>
<a class="ui link button" href="/yooome/golang/tags">Manage</a>
</div>
</div>
</div>
<div class='tab scrolling menu' data-tab='branches' id='branches_panel'>
<div data-value="main" class="item" title="main"><span class="iconify" data-icon="gitee:branch" style="font-size: 13px;margin-right:4px; color:#8C92A4"></span> <span>main</span></div>
</div>
</div>
</div>
<style>
  .iconfont.icon-shieldlock {
    color: #8c92a4;
  }
  .dropdown-search-icon {
    position: absolute;
    top: 8px;
    left: 11px;
  }
</style>
<style>
  #git-project-branch .project-branch-tab-menu, .project-branch-item .project-branch-tab-menu {
    padding-left: 0px !important;
    padding-right: 0px !important;
    margin: 0 11px !important;
    border-bottom: 1px solid #dfe3e9 !important; }
  #git-project-branch .ui.dropdown .menu, .project-branch-item .ui.dropdown .menu {
    width: 360px !important; }
    #git-project-branch .ui.dropdown .menu .item, .project-branch-item .ui.dropdown .menu .item {
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap; }
  #git-project-branch .tab-menu-actions, .project-branch-item .tab-menu-actions {
    position: absolute;
    right: 0px !important;
    bottom: 0.357em; }
  #git-project-branch .tab-menu-action, .project-branch-item .tab-menu-action {
    position: relative !important;
    right: 0px !important;
    bottom: 0px !important; }
  #git-project-branch .menu::after, .project-branch-item .menu::after {
    display: none !important; }
</style>
<script>
  var $branchesDropdown = $('#branches_panel');
  var $tagsDropdown = $('#tags_panel');
  var $searchNameInput = $('.search-branch');
  var concurrentRequestLock = false;
  var filterXSS = window.filterXSS;
  var search_text = "";
  var branch_page_number = 1;
  var branch_total_pager = Math.ceil(1 / 20) || 1
  
  var flag_is_loading = false;
  var flag_page_number = 1;
  var flag_total_pager = Math.ceil(0 / 20) || 1
  
  $branchesDropdown.scroll(function() {
    var branchesPanel = document.getElementById('branches_panel');
    var numOfBranches = $branchesDropdown.children().length;
    if (branchesPanel.clientHeight + branchesPanel.scrollTop + 37 > branchesPanel.scrollHeight && numOfBranches < 1) {
      debounceLoadMoreBranches.call();
    }
  });
  function resetFlagVal() {
    flag_is_loading = false;
    flag_page_number = 1;
    flag_total_pager = 1;
  
    concurrentRequestLock = false
    search_text = "";
    branch_page_number = 1;
    branch_total_pager = 1
  }
  $searchNameInput.on('input', window.globalUtils.debouce(function (e) {
    resetFlagVal()
    var $currentTab = $('.tab-menu-action.active');
    var numOfBranches = $branchesDropdown.children().length;
    var searchWord = $searchNameInput.val().trim();
    search_text = searchWord
    if($currentTab.data('tab') === 'branches') {
      if (searchWord !== "") {
        loadData(searchWord,1);
      } else {
        loadData();
      }
    }
    var numOfTags = $tagsDropdown.children().length;
    if($currentTab.data('tab') === 'tags') {
      if (searchWord !== "") {
        fetchTags(searchWord,1);
      } else {
        fetchTags();
      }
    }
  }, 500));
  
  function toggleNoResultView($popPanel) {
    let no_data_html= `<div class='mt-1 mb-1 d-flex-center'> <span>暂无数据</span> </div>`
    $popPanel.append(no_data_html)
  }
  var debounceLoadMoreBranches = window.globalUtils.debouce(function () {
    if (concurrentRequestLock) return;
    branch_page_number += 1;
    if (branch_page_number > branch_total_pager) return;
    loadData(search_text, branch_page_number);
  }, 350);
  
  function loadData(search, page) {
    if (concurrentRequestLock) { return; }
    concurrentRequestLock = true;
  
    var searchParams = search || "";
    var pageParams = page || 1;
    $.ajax({
      url: "/" + gon.user_project + "/branches/names.json",
      type: 'GET',
      data: {
        search: searchParams,
        page: pageParams,
      },
      dataType: 'json',
      success: function (data) {
        branch_total_pager = data.total_pages;
        var html = '';
  
        if (pageParams === 1) {
          $branchesDropdown.empty();
        }
        data.branches.forEach(function (branch) {
          var protectRule = '';
          var branchName = filterXSS(branch.name);
          var icon = 'gitee:branch'
          if(branch.branch_type.value === 1) {
            var rule = filterXSS(branch.protection_rule.wildcard);
            protectRule = `<i
                class="iconfont icon-shieldlock protected-branch-popup"
                data-title="受保护分支"
                data-content='保护规则： ${rule}'
              >
              </i>`
            icon ='gitee:pen-lock'
          }else if(branch.branch_type.value === 2) {
            icon ='gitee:pen-ban'
          }
          var branchIcon = `<span class="iconify" data-icon=${icon} style="font-size: 13px; margin-right:4px; color:#8C92A4"></span>`
          html += `<div data-value='${branchName}' class="item">
                    ${branchIcon} 
                    <span>${branchName}</span> ${protectRule}
                    </div>`
        });
        $branchesDropdown.append(html);
        $('.protected-branch-popup').popup()
        if (pageParams === 1 && data.count === 0) {
          toggleNoResultView($branchesDropdown);
        }
      },
      complete: function () {
        concurrentRequestLock = false;
      }
    });
  }
  
  
  
  $tagsDropdown.scroll(function() {
    var tagsPanel = document.getElementById('tags_panel');
    var numOfTags = $tagsDropdown.children().length;
    if (tagsPanel.clientHeight + tagsPanel.scrollTop + 37 > tagsPanel.scrollHeight && numOfTags < 0) {
      debounceLoadMore.call();
    }
  });
  var debounceLoadMore = window.globalUtils.debouce(function () {
    if (flag_is_loading) return;
    flag_page_number += 1;
    if (flag_page_number > flag_total_pager) return;
    fetchTags(search_text, flag_page_number);
  }, 350);
  
  function fetchTags(search, page) {
    var searchParams = search || "";
    var pageParams = page || 1;
  
    if (flag_is_loading) return;
    flag_is_loading = true;
  
    $.ajax({
      url: "/" + gon.user_project + "/tags/names.json",
      data: {
        search: searchParams,
        page: pageParams,
      },
      type: "GET",
      xhrFields: {
        withCredentials: true,
      },
      success: function (data) {
        flag_total_pager = data.total_pages;
        if (pageParams === 1) {
          $tagsDropdown.html('');
        }
        data.tags.forEach((tag) => {
          const itemDiv = document.createElement('div');
          itemDiv.classList.add('item');
          itemDiv.setAttribute('data-value', tag.name);
          itemDiv.innerText = window.filterXSS(tag.name);
          $tagsDropdown.append(itemDiv)
        });
        if (pageParams === 1 && data.count === 0) {
          toggleNoResultView($tagsDropdown);
        }
      },
      error: function () {
      },
      complete: function () {
        flag_is_loading = false;
      },
    });
  }
  $('.project-branch-tab-menu').on('click','.tab-menu-item', function (e) {
    var $currentTab = $(this).data('tab')
    if($currentTab === 'branches') {
      $searchNameInput.val('')
      search_text = '';
      loadData()
    }
    if($currentTab === 'tags') {
      $searchNameInput.val('')
      search_text = '';
      fetchTags();
    }
  })
</script>

<script>
  $(function () {
    var curNode = $('.git-project-branch-item')
    if (true ){
      curNode = $('.left-project-branch-item')
    }else {
      curNode = $('.git-project-branch-item')
    }
    Gitee.initTabsInDropdown(curNode.find('#git-project-branch').dropdown({
      fullTextSearch: true,
      selectOnKeydown: false,
      direction: 'downward',
      action: function (text,value,el) {
        var oItemOrInitObject = el[0] || el
        var isNotSelect = oItemOrInitObject.dataset.tab && oItemOrInitObject.dataset.tab === 'branches'
        if(isNotSelect){
          console.warn("You didn't choose a branch")
          return
        }
        var path = $('#path').val();
        var href = ['/yooome/golang/tree', encodeURIComponent(value), path].join('/');
        window.location.href = href;
        return true
      },
      onNoResults: function (searchTerm) {
        //未找到结果
        return true
      },
    }));
    $('.protected-branch-popup').popup()
  })
</script>

</div>
</div>
<div class='tree-breadcrumb-wrapper'>
<a data-direction="back" class="section repo-name" style="font-weight: bold" href="/yooome/golang/tree/main">golang
</a><div class='divider'>
/
</div>
<strong>
<a data-direction="back" data-path="21-k8s详细教程" class="section cblue" href="/yooome/golang/tree/main/21-k8s%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B">21-k8s详细教程
</a></strong>
<div class='divider'>
/
</div>
<strong>
Kubernetes详细教程.md
</strong>
<i class='iconfont icon-clone ml-1' data-clipboard-text='21-k8s详细教程/Kubernetes详细教程.md' id='btn-copy-file-path'></i>
</div>
</div>
<style>
  #btn-copy-file-path {
    vertical-align: middle;
    cursor: pointer;
  }
  .file-iconify-item {
      display: inline-block !important;
      cursor: pointer;
      border-radius: 4px;
      margin-right: 8px;
      cursor: pointer;
      width: 32px;
      height: 32px;
      text-align: center;
      &:hover {
        background-color: #F5F7FA
      }
    }
  .dropdown.project-branch-item {
    #git-project-branch {
      min-width: 92px !important;
    }
    .icon.dropdown {
      float: right !important;
      margin-top: 2px !important
    }
    .ui.dropdown .menu.transition.visible {
      min-width: 288px !important;
      max-width: 360px !important
      .item {
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
      }
    }
  }
</style>
<script>
  $btnCopy = $('#btn-copy-file-path')
  $btnCopy.popup({
    content: 'Copy path'
  })
  
  if ($btnCopy[0]) {
    new Clipboard($btnCopy[0]).on('success', function() {
      $btnCopy.popup('destroy').popup({
        content: 'Copied',
        on: 'manual'
      }).popup('show');
      setTimeout(function () {
        $btnCopy.popup('destroy').popup({
          content: 'Copy path'
        });
      }, 2000)
    });
  }
</script>


</div>
<div class='ui horizontal list repo-action-list branches-tags' style='display: none;'>
<div class='item'>
<a class="ui blank button" href="/yooome/golang/branches"><i class='iconfont icon-branches'></i>
Branches 1
</a></div>
<div class='item mr-3'>
<a class="ui blank button" href="/yooome/golang/tags"><i class='iconfont icon-tag'></i>
Tags 0
</a></div>
</div>
</div>
<script src="https://cn-assets.gitee.com/webpacks/parse_blob_form_scheme-38e5ca827671ce5f7c16.bundle.js"></script>
<script>
  if(window.gon.locale == 'en')
    $('.branches-tags').css('margin-top', '12px')
   // 仓库页面切换路径时: 刷新 yaml 错误检查
  $(window).on('pjax-complete:file-show', function () {
    window.parseBlobFormScheme && window.parseBlobFormScheme($('.js-blob-data').data('blob'));
  });
</script>

<style>
  .ui.dropdown .menu > .header {
    text-transform: none; }
</style>
<script>
  $(function () {
    var $tip = $('#apk-download-tip');
    if (!$tip.length) {
      return;
    }
    $tip.find('.btn-close').on('click', function () {
      $tip.hide();
    });
  });
  (function(){
    function pathAutoRender() {
      var $parent = $('#git-project-bread'),
          $child = $('#git-project-bread').children('.ui.horizontal.list'),
          mainWidth = 0;
      $child.each(function (i,item) {
        mainWidth += $(item).width()
      });
      $('.breadcrumb.path.fork-path').remove();
      if (mainWidth > 995) {
        $('#path-breadcrumb').hide();
        $parent.append('<div class="ui breadcrumb path fork-path">' + $('#path-breadcrumb').html() + '<div/>')
      } else {
        $('#path-breadcrumb').show();
      }
    }
    window.pathAutoRender = pathAutoRender;
    pathAutoRender();
  })();
</script>

<div class='row column tree-holder' id='tree-holder'>
<div class='tree-content-holder' id='tree-content-holder'>
<div class='file_holder'>
<div class='file_title'>
<div class='blob-header-title'>
<div class='blob-description'>
<i class="iconfont icon-file"></i>
<span class='file_name' title='Kubernetes详细教程.md'>
Kubernetes详细教程.md
</span>
<small>213.79 KB</small>
</div>
<div class='options'><div class='ui mini buttons basic'>
<textarea name="blob_raw" id="blob_raw" style="display:none;">
## 							Kubernetes详细教程&#x000A;&#x000A;### 1. Kubernetes介绍&#x000A;&#x000A;#### 1.1 应用部署方式演变&#x000A;&#x000A;在部署应用程序的方式上，主要经历了三个时代：&#x000A;&#x000A;- **传统部署**：互联网早期，会直接将应用程序部署在物理机上&#x000A;&#x000A;  &gt; 优点：简单，不需要其它技术的参与&#x000A;  &gt;&#x000A;  &gt; 缺点：不能为应用程序定义资源使用边界，很难合理地分配计算资源，而且程序之间容易产生影响&#x000A;&#x000A;- **虚拟化部署**：可以在一台物理机上运行多个虚拟机，每个虚拟机都是独立的一个环境&#x000A;&#x000A;  &gt; 优点：程序环境不会相互产生影响，提供了一定程度的安全性&#x000A;  &gt;&#x000A;  &gt; 缺点：增加了操作系统，浪费了部分资源&#x000A;&#x000A;- **容器化部署**：与虚拟化类似，但是共享了操作系统&#x000A;&#x000A;  &gt; 优点：&#x000A;  &gt;&#x000A;  &gt; 可以保证每个容器拥有自己的文件系统、CPU、内存、进程空间等&#x000A;  &gt;&#x000A;  &gt; 运行应用程序所需要的资源都被容器包装，并和底层基础架构解耦&#x000A;  &gt;&#x000A;  &gt; 容器化的应用程序可以跨云服务商、跨Linux操作系统发行版进行部署&#x000A;&#x000A;![image-20200505183738289](./images/image-20200505183738289.png)&#x000A;&#x000A;容器化部署方式给带来很多的便利，但是也会出现一些问题，比如说：&#x000A;&#x000A;- 一个容器故障停机了，怎么样让另外一个容器立刻启动去替补停机的容器&#x000A;- 当并发访问量变大的时候，怎么样做到横向扩展容器数量&#x000A;&#x000A;这些容器管理的问题统称为**容器编排**问题，为了解决这些容器编排问题，就产生了一些容器编排的软件：&#x000A;&#x000A;- **Swarm**：Docker自己的容器编排工具&#x000A;- **Mesos**：Apache的一个资源统一管控的工具，需要和Marathon结合使用&#x000A;- **Kubernetes**：Google开源的的容器编排工具&#x000A;&#x000A;![image-20200524150339551](images/image-20200524150339551.png)&#x000A;&#x000A;#### 1.2 kubernetes简介&#x000A;&#x000A;![image-20200406232838722](./Kubenetes.assets/image-20200406232838722.png)&#x000A;&#x000A; &#x000A;&#x000A;kubernetes，是一个全新的基于容器技术的分布式架构领先方案，是谷歌严格保密十几年的秘密武器----Borg系统的一个开源版本，于2014年9月发布第一个版本，2015年7月发布第一个正式版本。&#x000A;&#x000A;kubernetes的本质是**一组服务器集群**，它可以在集群的每个节点上运行特定的程序，来对节点中的容器进行管理。目的是实现资源管理的自动化，主要提供了如下的主要功能：&#x000A;&#x000A;- **自我修复**：一旦某一个容器崩溃，能够在1秒中左右迅速启动新的容器&#x000A;- **弹性伸缩**：可以根据需要，自动对集群中正在运行的容器数量进行调整&#x000A;- **服务发现**：服务可以通过自动发现的形式找到它所依赖的服务&#x000A;- **负载均衡**：如果一个服务起动了多个容器，能够自动实现请求的负载均衡&#x000A;- **版本回退**：如果发现新发布的程序版本有问题，可以立即回退到原来的版本&#x000A;- **存储编排**：可以根据容器自身的需求自动创建存储卷&#x000A;&#x000A;#### 1.3 kubernetes组件&#x000A;&#x000A;一个kubernetes集群主要是由**控制节点(master)**、**工作节点(node)**构成，每个节点上都会安装不同的组件。&#x000A;&#x000A;**master：集群的控制平面，负责集群的决策 ( 管理 )**&#x000A;&#x000A;&gt; **ApiServer** : 资源操作的唯一入口，接收用户输入的命令，提供认证、授权、API注册和发现等机制&#x000A;&gt;&#x000A;&gt; **Scheduler** : 负责集群资源调度，按照预定的调度策略将Pod调度到相应的node节点上&#x000A;&gt;&#x000A;&gt; **ControllerManager** : 负责维护集群的状态，比如程序部署安排、故障检测、自动扩展、滚动更新等&#x000A;&gt;&#x000A;&gt; **Etcd** ：负责存储集群中各种资源对象的信息&#x000A;&#x000A;**node：集群的数据平面，负责为容器提供运行环境 ( 干活 )**&#x000A;&#x000A;&gt; **Kubelet** : 负责维护容器的生命周期，即通过控制docker，来创建、更新、销毁容器&#x000A;&gt;&#x000A;&gt; **KubeProxy** : 负责提供集群内部的服务发现和负载均衡&#x000A;&gt;&#x000A;&gt; **Docker** : 负责节点上容器的各种操作&#x000A;&#x000A;![image-20200406184656917](images/image-20200406184656917.png)&#x000A;&#x000A;下面，以部署一个nginx服务来说明kubernetes系统各个组件调用关系：&#x000A;&#x000A;1. 首先要明确，一旦kubernetes环境启动之后，master和node都会将自身的信息存储到etcd数据库中&#x000A;&#x000A;2. 一个nginx服务的安装请求会首先被发送到master节点的apiServer组件&#x000A;&#x000A;3. apiServer组件会调用scheduler组件来决定到底应该把这个服务安装到哪个node节点上&#x000A;&#x000A;   在此时，它会从etcd中读取各个node节点的信息，然后按照一定的算法进行选择，并将结果告知apiServer&#x000A;&#x000A;4. apiServer调用controller-manager去调度Node节点安装nginx服务&#x000A;&#x000A;5. kubelet接收到指令后，会通知docker，然后由docker来启动一个nginx的pod&#x000A;&#x000A;   pod是kubernetes的最小操作单元，容器必须跑在pod中至此，&#x000A;&#x000A;6. 一个nginx服务就运行了，如果需要访问nginx，就需要通过kube-proxy来对pod产生访问的代理&#x000A;&#x000A;这样，外界用户就可以访问集群中的nginx服务了&#x000A;&#x000A;#### 1.4 kubernetes概念&#x000A;&#x000A;**Master**：集群控制节点，每个集群需要至少一个master节点负责集群的管控&#x000A;&#x000A;**Node**：工作负载节点，由master分配容器到这些node工作节点上，然后node节点上的docker负责容器的运行&#x000A;&#x000A;**Pod**：kubernetes的最小控制单元，容器都是运行在pod中的，一个pod中可以有1个或者多个容器&#x000A;&#x000A;**Controller**：控制器，通过它来实现对pod的管理，比如启动pod、停止pod、伸缩pod的数量等等&#x000A;&#x000A;**Service**：pod对外服务的统一入口，下面可以维护者同一类的多个pod&#x000A;&#x000A;**Label**：标签，用于对pod进行分类，同一类pod会拥有相同的标签&#x000A;&#x000A;**NameSpace**：命名空间，用来隔离pod的运行环境&#x000A;&#x000A;### 2. kubernetes集群环境搭建&#x000A;&#x000A;#### 2.1 前置知识点&#x000A;&#x000A;目前生产部署Kubernetes 集群主要有两种方式：&#x000A;&#x000A;**kubeadm**&#x000A;&#x000A;Kubeadm 是一个K8s 部署工具，提供kubeadm init 和kubeadm join，用于快速部署Kubernetes 集群。&#x000A;&#x000A;官方地址：https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm/&#x000A;&#x000A;**二进制包**&#x000A;&#x000A;从github 下载发行版的二进制包，手动部署每个组件，组成Kubernetes 集群。&#x000A;&#x000A;Kubeadm 降低部署门槛，但屏蔽了很多细节，遇到问题很难排查。如果想更容易可控，推荐使用二进制包部署Kubernetes 集群，虽然手动部署麻烦点，期间可以学习很多工作原理，也利于后期维护。&#x000A;&#x000A;![image-20200404094800622](images/image-20200404094800622.png)&#x000A;&#x000A;#### 2.2 kubeadm 部署方式介绍&#x000A;&#x000A;kubeadm 是官方社区推出的一个用于快速部署kubernetes 集群的工具，这个工具能通过两条指令完成一个kubernetes 集群的部署：&#x000A;&#x000A;- 创建一个Master 节点kubeadm init&#x000A;- 将Node 节点加入到当前集群中$ kubeadm join &lt;Master 节点的IP 和端口&gt;&#x000A;&#x000A;#### 2.3 安装要求&#x000A;&#x000A;在开始之前，部署Kubernetes 集群机器需要满足以下几个条件：&#x000A;&#x000A;- 一台或多台机器，操作系统CentOS7.x-86_x64&#x000A;- 硬件配置：2GB 或更多RAM，2 个CPU 或更多CPU，硬盘30GB 或更多&#x000A;- 集群中所有机器之间网络互通&#x000A;- 可以访问外网，需要拉取镜像&#x000A;- 禁止swap 分区&#x000A;&#x000A;#### 2.4 最终目标&#x000A;&#x000A;- 在所有节点上安装Docker 和kubeadm&#x000A;- 部署Kubernetes Master&#x000A;- 部署容器网络插件&#x000A;- 部署Kubernetes Node，将节点加入Kubernetes 集群中&#x000A;- 部署Dashboard Web 页面，可视化查看Kubernetes 资源&#x000A;&#x000A;#### 2.5 准备环境 &#x000A;&#x000A;![image-20210609000002940](images/image-20210609000002940.png)&#x000A;&#x000A;| 角色     | IP地址      | 组件                              |&#x000A;| :------- | :---------- | :-------------------------------- |&#x000A;| master01 | 192.168.5.3 | docker，kubectl，kubeadm，kubelet |&#x000A;| node01   | 192.168.5.4 | docker，kubectl，kubeadm，kubelet |&#x000A;| node02   | 192.168.5.5 | docker，kubectl，kubeadm，kubelet |&#x000A;&#x000A;#### 2.6 环境初始化&#x000A;&#x000A;##### 2.6.1 检查操作系统的版本&#x000A;&#x000A;```powershell&#x000A;# 此方式下安装kubernetes集群要求Centos版本要在7.5或之上&#x000A;[root@master ~]# cat /etc/redhat-release&#x000A;Centos Linux 7.5.1804 (Core)&#x000A;```&#x000A;&#x000A;##### 2.6.2 主机名解析&#x000A;&#x000A;为了方便集群节点间的直接调用，在这个配置一下主机名解析，企业中推荐使用内部DNS服务器&#x000A;&#x000A;```powershell&#x000A;# 主机名成解析 编辑三台服务器的/etc/hosts文件，添加下面内容&#x000A;192.168.90.100 master&#x000A;192.168.90.106 node1&#x000A;192.168.90.107 node2&#x000A;```&#x000A;&#x000A;##### 2.6.3 时间同步&#x000A;&#x000A;kubernetes要求集群中的节点时间必须精确一直，这里使用chronyd服务从网络同步时间&#x000A;&#x000A;企业中建议配置内部的会见同步服务器&#x000A;&#x000A;```powershell&#x000A;# 启动chronyd服务&#x000A;[root@master ~]# systemctl start chronyd&#x000A;[root@master ~]# systemctl enable chronyd&#x000A;[root@master ~]# date&#x000A;```&#x000A;&#x000A;##### 2.6.4  禁用iptable和firewalld服务&#x000A;&#x000A;kubernetes和docker 在运行的中会产生大量的iptables规则，为了不让系统规则跟它们混淆，直接关闭系统的规则&#x000A;&#x000A;```powershell&#x000A;# 1 关闭firewalld服务&#x000A;[root@master ~]# systemctl stop firewalld&#x000A;[root@master ~]# systemctl disable firewalld&#x000A;# 2 关闭iptables服务&#x000A;[root@master ~]# systemctl stop iptables&#x000A;[root@master ~]# systemctl disable iptables&#x000A;```&#x000A;&#x000A;##### 2.6.5 禁用selinux&#x000A;&#x000A;selinux是linux系统下的一个安全服务，如果不关闭它，在安装集群中会产生各种各样的奇葩问题&#x000A;&#x000A;```powershell&#x000A;# 编辑 /etc/selinux/config 文件，修改SELINUX的值为disable&#x000A;# 注意修改完毕之后需要重启linux服务&#x000A;SELINUX=disabled&#x000A;```&#x000A;&#x000A;##### 2.6.6 禁用swap分区&#x000A;&#x000A;swap分区指的是虚拟内存分区，它的作用是物理内存使用完，之后将磁盘空间虚拟成内存来使用，启用swap设备会对系统的性能产生非常负面的影响，因此kubernetes要求每个节点都要禁用swap设备，但是如果因为某些原因确实不能关闭swap分区，就需要在集群安装过程中通过明确的参数进行配置说明&#x000A;&#x000A;```powershell&#x000A;# 编辑分区配置文件/etc/fstab，注释掉swap分区一行&#x000A;# 注意修改完毕之后需要重启linux服务&#x000A;vim /etc/fstab&#x000A;注释掉 /dev/mapper/centos-swap swap&#x000A;# /dev/mapper/centos-swap swap&#x000A;```&#x000A;&#x000A;##### 2.6.7 修改linux的内核参数&#x000A;&#x000A;```powershell&#x000A;# 修改linux的内核采纳数，添加网桥过滤和地址转发功能&#x000A;# 编辑/etc/sysctl.d/kubernetes.conf文件，添加如下配置：&#x000A;net.bridge.bridge-nf-call-ip6tables = 1&#x000A;net.bridge.bridge-nf-call-iptables = 1&#x000A;net.ipv4.ip_forward = 1&#x000A;&#x000A;# 重新加载配置&#x000A;[root@master ~]# sysctl -p&#x000A;# 加载网桥过滤模块&#x000A;[root@master ~]# modprobe br_netfilter&#x000A;# 查看网桥过滤模块是否加载成功&#x000A;[root@master ~]# lsmod | grep br_netfilter&#x000A;```&#x000A;&#x000A;##### 2.6.8 配置ipvs功能&#x000A;&#x000A;在Kubernetes中Service有两种带来模型，一种是基于iptables的，一种是基于ipvs的两者比较的话，ipvs的性能明显要高一些，但是如果要使用它，需要手动载入ipvs模块&#x000A;&#x000A;```powershell&#x000A;# 1.安装ipset和ipvsadm&#x000A;[root@master ~]# yum install ipset ipvsadm -y&#x000A;# 2.添加需要加载的模块写入脚本文件&#x000A;[root@master ~]# cat &lt;&lt;EOF&gt; /etc/sysconfig/modules/ipvs.modules&#x000A;#!/bin/bash&#x000A;modprobe -- ip_vs&#x000A;modprobe -- ip_vs_rr&#x000A;modprobe -- ip_vs_wrr&#x000A;modprobe -- ip_vs_sh&#x000A;modprobe -- nf_conntrack_ipv4&#x000A;EOF&#x000A;# 3.为脚本添加执行权限&#x000A;[root@master ~]# chmod +x /etc/sysconfig/modules/ipvs.modules&#x000A;# 4.执行脚本文件&#x000A;[root@master ~]# /bin/bash /etc/sysconfig/modules/ipvs.modules&#x000A;# 5.查看对应的模块是否加载成功&#x000A;[root@master ~]# lsmod | grep -e ip_vs -e nf_conntrack_ipv4&#x000A;```&#x000A;&#x000A;##### 2.6.9 安装docker&#x000A;&#x000A;```powershell&#x000A;# 1、切换镜像源&#x000A;[root@master ~]# wget https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo -O /etc/yum.repos.d/docker-ce.repo&#x000A;&#x000A;# 2、查看当前镜像源中支持的docker版本&#x000A;[root@master ~]# yum list docker-ce --showduplicates&#x000A;&#x000A;# 3、安装特定版本的docker-ce&#x000A;# 必须制定--setopt=obsoletes=0，否则yum会自动安装更高版本&#x000A;[root@master ~]# yum install --setopt=obsoletes=0 docker-ce-18.06.3.ce-3.el7 -y&#x000A;&#x000A;# 4、添加一个配置文件&#x000A;#Docker 在默认情况下使用Vgroup Driver为cgroupfs，而Kubernetes推荐使用systemd来替代cgroupfs&#x000A;[root@master ~]# mkdir /etc/docker&#x000A;[root@master ~]# cat &lt;&lt;EOF&gt; /etc/docker/daemon.json&#x000A;{&#x000A;	&quot;exec-opts&quot;: [&quot;native.cgroupdriver=systemd&quot;],&#x000A;	&quot;registry-mirrors&quot;: [&quot;https://kn0t2bca.mirror.aliyuncs.com&quot;]&#x000A;}&#x000A;EOF&#x000A;&#x000A;# 5、启动dokcer&#x000A;[root@master ~]# systemctl restart docker&#x000A;[root@master ~]# systemctl enable docker&#x000A;```&#x000A;&#x000A;##### 2.6.10 安装Kubernetes组件&#x000A;&#x000A;```powershell&#x000A;# 1、由于kubernetes的镜像在国外，速度比较慢，这里切换成国内的镜像源&#x000A;# 2、编辑/etc/yum.repos.d/kubernetes.repo,添加下面的配置&#x000A;[kubernetes]&#x000A;name=Kubernetes&#x000A;baseurl=http://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64&#x000A;enabled=1&#x000A;gpgchech=0&#x000A;repo_gpgcheck=0&#x000A;gpgkey=http://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg&#x000A;			http://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg&#x000A;&#x000A;# 3、安装kubeadm、kubelet和kubectl&#x000A;[root@master ~]# yum install --setopt=obsoletes=0 kubeadm-1.17.4-0 kubelet-1.17.4-0 kubectl-1.17.4-0 -y&#x000A;&#x000A;# 4、配置kubelet的cgroup&#x000A;#编辑/etc/sysconfig/kubelet, 添加下面的配置&#x000A;KUBELET_CGROUP_ARGS=&quot;--cgroup-driver=systemd&quot;&#x000A;KUBE_PROXY_MODE=&quot;ipvs&quot;&#x000A;&#x000A;# 5、设置kubelet开机自启&#x000A;[root@master ~]# systemctl enable kubelet&#x000A;```&#x000A;&#x000A;##### 2.6.11 准备集群镜像&#x000A;&#x000A;```powershell&#x000A;# 在安装kubernetes集群之前，必须要提前准备好集群需要的镜像，所需镜像可以通过下面命令查看&#x000A;[root@master ~]# kubeadm config images list&#x000A;&#x000A;# 下载镜像&#x000A;# 此镜像kubernetes的仓库中，由于网络原因，无法连接，下面提供了一种替换方案&#x000A;images=(&#x000A;	kube-apiserver:v1.17.4&#x000A;	kube-controller-manager:v1.17.4&#x000A;	kube-scheduler:v1.17.4&#x000A;	kube-proxy:v1.17.4&#x000A;	pause:3.1&#x000A;	etcd:3.4.3-0&#x000A;	coredns:1.6.5&#x000A;)&#x000A;&#x000A;for imageName in ${images[@]};do&#x000A;	docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/$imageName&#x000A;	docker tag registry.cn-hangzhou.aliyuncs.com/google_containers/$imageName k8s.gcr.io/$imageName&#x000A;	docker rmi registry.cn-hangzhou.aliyuncs.com/google_containers/$imageName &#x000A;done&#x000A;&#x000A;```&#x000A;&#x000A;##### 2.6.11 集群初始化&#x000A;&#x000A;&gt;下面的操作只需要在master节点上执行即可&#x000A;&#x000A;```powershell&#x000A;# 创建集群&#x000A;[root@master ~]# kubeadm init \&#x000A;	--apiserver-advertise-address=192.168.90.100 \&#x000A;	--image-repository registry.aliyuncs.com/google_containers \&#x000A;	--kubernetes-version=v1.17.4 \&#x000A;	--service-cidr=10.96.0.0/12 \&#x000A;	--pod-network-cidr=10.244.0.0/16&#x000A;# 创建必要文件&#x000A;[root@master ~]# mkdir -p $HOME/.kube&#x000A;[root@master ~]# sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config&#x000A;[root@master ~]# sudo chown $(id -u):$(id -g) $HOME/.kube/config&#x000A;```&#x000A;&#x000A;&gt; 下面的操作只需要在node节点上执行即可&#x000A;&#x000A;```powershell&#x000A;kubeadm join 192.168.0.100:6443 --token awk15p.t6bamck54w69u4s8 \&#x000A;    --discovery-token-ca-cert-hash sha256:a94fa09562466d32d29523ab6cff122186f1127599fa4dcd5fa0152694f17117 &#x000A;```&#x000A;&#x000A;在master上查看节点信息&#x000A;&#x000A;```powershell&#x000A;[root@master ~]# kubectl get nodes&#x000A;NAME    STATUS   ROLES     AGE   VERSION&#x000A;master  NotReady  master   6m    v1.17.4&#x000A;node1   NotReady   &lt;none&gt;  22s   v1.17.4&#x000A;node2   NotReady   &lt;none&gt;  19s   v1.17.4&#x000A;```&#x000A;&#x000A;##### 2.6.13 安装网络插件，只在master节点操作即可&#x000A;&#x000A;```powershell&#x000A;wget https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml&#x000A;```&#x000A;&#x000A;由于外网不好访问，如果出现无法访问的情况，可以直接用下面的 记得文件名是kube-flannel.yml，位置：/root/kube-flannel.yml内容：&#x000A;&#x000A;```powershell&#x000A;https://github.com/flannel-io/flannel/tree/master/Documentation/kube-flannel.yml&#x000A;```&#x000A;也可手动拉取指定版本&#x000A;docker pull quay.io/coreos/flannel:v0.14.0              #拉取flannel网络，三台主机&#x000A;docker images                  #查看仓库是否拉去下来&#x000A;&#x000A;```个人笔记```&#x000A;若是集群状态一直是 notready,用下面语句查看原因，&#x000A;journalctl -f -u kubelet.service&#x000A;若原因是： cni.go:237] Unable to update cni config: no networks found in /etc/cni/net.d&#x000A;mkdir -p /etc/cni/net.d                    #创建目录给flannel做配置文件&#x000A;vim /etc/cni/net.d/10-flannel.conf         #编写配置文件&#x000A;```powershell&#x000A;&#x000A;{&#x000A; &quot;name&quot;:&quot;cbr0&quot;,&#x000A; &quot;cniVersion&quot;:&quot;0.3.1&quot;,&#x000A; &quot;type&quot;:&quot;flannel&quot;,&#x000A; &quot;deledate&quot;:{&#x000A;    &quot;hairpinMode&quot;:true,&#x000A;    &quot;isDefaultGateway&quot;:true&#x000A;  }&#x000A;&#x000A;}&#x000A;&#x000A;```&#x000A;&#x000A;&#x000A;##### 2.6.14 使用kubeadm reset重置集群&#x000A;&#x000A;```&#x000A;#在master节点之外的节点进行操作&#x000A;kubeadm reset&#x000A;systemctl stop kubelet&#x000A;systemctl stop docker&#x000A;rm -rf /var/lib/cni/&#x000A;rm -rf /var/lib/kubelet/*&#x000A;rm -rf /etc/cni/&#x000A;ifconfig cni0 down&#x000A;ifconfig flannel.1 down&#x000A;ifconfig docker0 down&#x000A;ip link delete cni0&#x000A;ip link delete flannel.1&#x000A;##重启kubelet&#x000A;systemctl restart kubelet&#x000A;##重启docker&#x000A;systemctl restart docker&#x000A;```&#x000A;&#x000A;##### 2.6.15 重启kubelet和docker&#x000A;&#x000A;```powershell&#x000A;# 重启kubelet&#x000A;systemctl restart kubelet&#x000A;# 重启docker&#x000A;systemctl restart docker&#x000A;```&#x000A;&#x000A;使用配置文件启动fannel&#x000A;&#x000A;```powershell&#x000A;kubectl apply -f kube-flannel.yml&#x000A;```&#x000A;&#x000A;等待它安装完毕 发现已经是 集群的状态已经是Ready&#x000A;&#x000A;![img](images/2232696-20210621233106024-1676033717.png)&#x000A;&#x000A;##### 2.6.16 kubeadm中的命令&#x000A;&#x000A;```powershell&#x000A;# 生成 新的token&#x000A;[root@master ~]# kubeadm token create --print-join-command&#x000A;```&#x000A;&#x000A;#### 2.7 集群测试&#x000A;&#x000A;##### 2.7.1 创建一个nginx服务&#x000A;&#x000A;```powershell&#x000A;kubectl create deployment nginx  --image=nginx:1.14-alpine&#x000A;```&#x000A;&#x000A;##### 2.7.2 暴露端口&#x000A;&#x000A;```powershell&#x000A;kubectl expose deploy nginx  --port=80 --target-port=80  --type=NodePort&#x000A;```&#x000A;&#x000A;##### 2.7.3 查看服务&#x000A;&#x000A;```powershell&#x000A;kubectl get pod,svc&#x000A;```&#x000A;&#x000A;##### 2.7.4 查看pod&#x000A;&#x000A;![2232696-20210621233130477-111035427](images/2232696-20210621233130477-111035427.png)&#x000A;&#x000A;浏览器测试结果：&#x000A;&#x000A;![img](images/2232696-20210621233157075-1117518703.png)&#x000A;&#x000A;### 3. 资源管理&#x000A;&#x000A;#### 3.1 资源管理介绍&#x000A;&#x000A;在kubernetes中，所有的内容都抽象为资源，用户需要通过操作资源来管理kubernetes。&#x000A;&#x000A;&gt; kubernetes的本质上就是一个集群系统，用户可以在集群中部署各种服务，所谓的部署服务，其实就是在kubernetes集群中运行一个个的容器，并将指定的程序跑在容器中。&#x000A;&gt;&#x000A;&gt; kubernetes的最小管理单元是pod而不是容器，所以只能将容器放在`Pod`中，而kubernetes一般也不会直接管理Pod，而是通过`Pod控制器`来管理Pod的。&#x000A;&gt;&#x000A;&gt; Pod可以提供服务之后，就要考虑如何访问Pod中服务，kubernetes提供了`Service`资源实现这个功能。&#x000A;&gt;&#x000A;&gt; 当然，如果Pod中程序的数据需要持久化，kubernetes还提供了各种`存储`系统。&#x000A;&#x000A;![image-20200406225334627](Kubenetes.assets/image-20200406225334627.png)&#x000A;&#x000A;&gt; 学习kubernetes的核心，就是学习如何对集群上的`Pod、Pod控制器、Service、存储`等各种资源进行操作&#x000A;&#x000A;#### 3.2 YAML语言介绍&#x000A;&#x000A;YAML是一个类似 XML、JSON 的标记性语言。它强调以**数据**为中心，并不是以标识语言为重点。因而YAML本身的定义比较简单，号称&quot;一种人性化的数据格式语言&quot;。&#x000A;&#x000A;```&#x000A;&lt;heima&gt;&#x000A;    &lt;age&gt;15&lt;/age&gt;&#x000A;    &lt;address&gt;Beijing&lt;/address&gt;&#x000A;&lt;/heima&gt;&#x000A;```&#x000A;&#x000A;```&#x000A;heima:&#x000A;  age: 15&#x000A;  address: Beijing&#x000A;```&#x000A;&#x000A;YAML的语法比较简单，主要有下面几个：&#x000A;&#x000A;- 大小写敏感&#x000A;- 使用缩进表示层级关系&#x000A;- 缩进不允许使用tab，只允许空格( 低版本限制 )&#x000A;- 缩进的空格数不重要，只要相同层级的元素左对齐即可&#x000A;- &#39;#&#39;表示注释&#x000A;&#x000A;YAML支持以下几种数据类型：&#x000A;&#x000A;- 纯量：单个的、不可再分的值&#x000A;- 对象：键值对的集合，又称为映射（mapping）/ 哈希（hash） / 字典（dictionary）&#x000A;- 数组：一组按次序排列的值，又称为序列（sequence） / 列表（list）&#x000A;&#x000A;```yml&#x000A;# 纯量, 就是指的一个简单的值，字符串、布尔值、整数、浮点数、Null、时间、日期&#x000A;# 1 布尔类型&#x000A;c1: true (或者True)&#x000A;# 2 整型&#x000A;c2: 234&#x000A;# 3 浮点型&#x000A;c3: 3.14&#x000A;# 4 null类型 &#x000A;c4: ~  # 使用~表示null&#x000A;# 5 日期类型&#x000A;c5: 2018-02-17    # 日期必须使用ISO 8601格式，即yyyy-MM-dd&#x000A;# 6 时间类型&#x000A;c6: 2018-02-17T15:02:31+08:00  # 时间使用ISO 8601格式，时间和日期之间使用T连接，最后使用+代表时区&#x000A;# 7 字符串类型&#x000A;c7: heima     # 简单写法，直接写值 , 如果字符串中间有特殊字符，必须使用双引号或者单引号包裹 &#x000A;c8: line1&#x000A;    line2     # 字符串过多的情况可以拆成多行，每一行会被转化成一个空格&#x000A;```&#x000A;&#x000A;&#x000A;&#x000A;```yaml&#x000A;# 对象&#x000A;# 形式一(推荐):&#x000A;heima:&#x000A;  age: 15&#x000A;  address: Beijing&#x000A;# 形式二(了解):&#x000A;heima: {age: 15,address: Beijing}&#x000A;```&#x000A;&#x000A;```yaml&#x000A;# 数组&#x000A;# 形式一(推荐):&#x000A;address:&#x000A;  - 顺义&#x000A;  - 昌平  &#x000A;# 形式二(了解):&#x000A;address: [顺义,昌平]&#x000A;```&#x000A;&#x000A;&gt; 小提示：&#x000A;&gt;&#x000A;&gt; 1 书写yaml切记`:` 后面要加一个空格&#x000A;&gt;&#x000A;&gt; 2 如果需要将多段yaml配置放在一个文件中，中间要使用`---`分隔&#x000A;&gt;&#x000A;&gt; 3 下面是一个yaml转json的网站，可以通过它验证yaml是否书写正确&#x000A;&gt;&#x000A;&gt; https://www.json2yaml.com/convert-yaml-to-json&#x000A;&#x000A;#### 3.3 资源管理方式&#x000A;&#x000A;- 命令式对象管理：直接使用命令去操作kubernetes资源&#x000A;&#x000A;  ``` powershell&#x000A;  kubectl run nginx-pod --image=nginx:1.17.1 --port=80&#x000A;  ```&#x000A;&#x000A;- 命令式对象配置：通过命令配置和配置文件去操作kubernetes资源&#x000A;&#x000A;  ```powershell&#x000A;  kubectl create/patch -f nginx-pod.yaml&#x000A;  ```&#x000A;&#x000A;- 声明式对象配置：通过apply命令和配置文件去操作kubernetes资源&#x000A;&#x000A;  ```powershell&#x000A;  kubectl apply -f nginx-pod.yaml&#x000A;  ```&#x000A;  &#x000A;  &#x000A;&#x000A;| 类型           | 操作对象 | 适用环境 | 优点           | 缺点                             |&#x000A;| :------------- | :------- | :------- | :------------- | :------------------------------- |&#x000A;| 命令式对象管理 | 对象     | 测试     | 简单           | 只能操作活动对象，无法审计、跟踪 |&#x000A;| 命令式对象配置 | 文件     | 开发     | 可以审计、跟踪 | 项目大时，配置文件多，操作麻烦   |&#x000A;| 声明式对象配置 | 目录     | 开发     | 支持目录操作   | 意外情况下难以调试               |&#x000A;&#x000A;##### 3.3.1 命令式对象管理&#x000A;&#x000A;**kubectl命令**&#x000A;&#x000A;kubectl是kubernetes集群的命令行工具，通过它能够对集群本身进行管理，并能够在集群上进行容器化应用的安装部署。kubectl命令的语法如下：&#x000A;&#x000A;```&#x000A;kubectl [command] [type] [name] [flags]&#x000A;```&#x000A;&#x000A;**comand**：指定要对资源执行的操作，例如create、get、delete&#x000A;&#x000A;**type**：指定资源类型，比如deployment、pod、service&#x000A;&#x000A;**name**：指定资源的名称，名称大小写敏感&#x000A;&#x000A;**flags**：指定额外的可选参数&#x000A;&#x000A;```shell&#x000A;# 查看所有pod&#x000A;kubectl get pod &#x000A;&#x000A;# 查看某个pod&#x000A;kubectl get pod pod_name&#x000A;&#x000A;# 查看某个pod,以yaml格式展示结果&#x000A;kubectl get pod pod_name -o yaml&#x000A;```&#x000A;&#x000A;**资源类型**&#x000A;&#x000A;kubernetes中所有的内容都抽象为资源，可以通过下面的命令进行查看:&#x000A;&#x000A;```&#x000A;kubectl api-resources&#x000A;```&#x000A;&#x000A;经常使用的资源有下面这些：&#x000A;&#x000A;| 资源分类      | 资源名称                 | 缩写    | 资源作用        |&#x000A;| :------------ | :----------------------- | :------ | :-------------- |&#x000A;| 集群级别资源  | nodes                    | no      | 集群组成部分    |&#x000A;| namespaces    | ns                       | 隔离Pod |                 |&#x000A;| pod资源       | pods                     | po      | 装载容器        |&#x000A;| pod资源控制器 | replicationcontrollers   | rc      | 控制pod资源     |&#x000A;|               | replicasets              | rs      | 控制pod资源     |&#x000A;|               | deployments              | deploy  | 控制pod资源     |&#x000A;|               | daemonsets               | ds      | 控制pod资源     |&#x000A;|               | jobs                     |         | 控制pod资源     |&#x000A;|               | cronjobs                 | cj      | 控制pod资源     |&#x000A;|               | horizontalpodautoscalers | hpa     | 控制pod资源     |&#x000A;|               | statefulsets             | sts     | 控制pod资源     |&#x000A;| 服务发现资源  | services                 | svc     | 统一pod对外接口 |&#x000A;|               | ingress                  | ing     | 统一pod对外接口 |&#x000A;| 存储资源      | volumeattachments        |         | 存储            |&#x000A;|               | persistentvolumes        | pv      | 存储            |&#x000A;|               | persistentvolumeclaims   | pvc     | 存储            |&#x000A;| 配置资源      | configmaps               | cm      | 配置            |&#x000A;|               | secrets                  |         | 配置            |&#x000A;&#x000A;**操作**&#x000A;&#x000A;kubernetes允许对资源进行多种操作，可以通过--help查看详细的操作命令&#x000A;&#x000A;```&#x000A;kubectl --help&#x000A;```&#x000A;&#x000A;经常使用的操作有下面这些：&#x000A;&#x000A;| 命令分类   | 命令         | 翻译                        | 命令作用                     |&#x000A;| :--------- | :----------- | :-------------------------- | :--------------------------- |&#x000A;| 基本命令   | create       | 创建                        | 创建一个资源                 |&#x000A;|            | edit         | 编辑                        | 编辑一个资源                 |&#x000A;|            | get          | 获取                        | 获取一个资源                 |&#x000A;|            | patch        | 更新                        | 更新一个资源                 |&#x000A;|            | delete       | 删除                        | 删除一个资源                 |&#x000A;|            | explain      | 解释                        | 展示资源文档                 |&#x000A;| 运行和调试 | run          | 运行                        | 在集群中运行一个指定的镜像   |&#x000A;|            | expose       | 暴露                        | 暴露资源为Service            |&#x000A;|            | describe     | 描述                        | 显示资源内部信息             |&#x000A;|            | logs         | 日志输出容器在 pod 中的日志 | 输出容器在 pod 中的日志      |&#x000A;|            | attach       | 缠绕进入运行中的容器        | 进入运行中的容器             |&#x000A;|            | exec         | 执行容器中的一个命令        | 执行容器中的一个命令         |&#x000A;|            | cp           | 复制                        | 在Pod内外复制文件            |&#x000A;|            | rollout      | 首次展示                    | 管理资源的发布               |&#x000A;|            | scale        | 规模                        | 扩(缩)容Pod的数量            |&#x000A;|            | autoscale    | 自动调整                    | 自动调整Pod的数量            |&#x000A;| 高级命令   | apply        | rc                          | 通过文件对资源进行配置       |&#x000A;|            | label        | 标签                        | 更新资源上的标签             |&#x000A;| 其他命令   | cluster-info | 集群信息                    | 显示集群信息                 |&#x000A;|            | version      | 版本                        | 显示当前Server和Client的版本 |&#x000A;&#x000A;下面以一个namespace / pod的创建和删除简单演示下命令的使用：&#x000A;&#x000A;```shell&#x000A;# 创建一个namespace&#x000A;[root@master ~]# kubectl create namespace dev&#x000A;namespace/dev created&#x000A;&#x000A;# 获取namespace&#x000A;[root@master ~]# kubectl get ns&#x000A;NAME              STATUS   AGE&#x000A;default           Active   21h&#x000A;dev               Active   21s&#x000A;kube-node-lease   Active   21h&#x000A;kube-public       Active   21h&#x000A;kube-system       Active   21h&#x000A;&#x000A;# 在此namespace下创建并运行一个nginx的Pod&#x000A;[root@master ~]# kubectl run pod --image=nginx:latest -n dev&#x000A;kubectl run --generator=deployment/apps.v1 is DEPRECATED and will be removed in a future version. Use kubectl run --generator=run-pod/v1 or kubectl create instead.&#x000A;deployment.apps/pod created&#x000A;&#x000A;# 查看新创建的pod&#x000A;[root@master ~]# kubectl get pod -n dev&#x000A;NAME  READY   STATUS    RESTARTS   AGE&#x000A;pod   1/1     Running   0          21s&#x000A;&#x000A;# 删除指定的pod&#x000A;[root@master ~]# kubectl delete pod pod-864f9875b9-pcw7x&#x000A;pod &quot;pod&quot; deleted&#x000A;&#x000A;# 删除指定的namespace&#x000A;[root@master ~]# kubectl delete ns dev&#x000A;namespace &quot;dev&quot; deleted&#x000A;```&#x000A;&#x000A;### 3.3.2 命令式对象配置&#x000A;&#x000A;命令式对象配置就是使用命令配合配置文件一起来操作kubernetes资源。&#x000A;&#x000A;1） 创建一个nginxpod.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Namespace&#x000A;metadata:&#x000A;  name: dev&#x000A;&#x000A;---&#x000A;&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: nginxpod&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx-containers&#x000A;    image: nginx:latest&#x000A;```&#x000A;&#x000A;2）执行create命令，创建资源：&#x000A;&#x000A;```powershell&#x000A;[root@master ~]# kubectl create -f nginxpod.yaml&#x000A;namespace/dev created&#x000A;pod/nginxpod created&#x000A;```&#x000A;&#x000A;此时发现创建了两个资源对象，分别是namespace和pod&#x000A;&#x000A;3）执行get命令，查看资源：&#x000A;&#x000A;```shell&#x000A;[root@master ~]#  kubectl get -f nginxpod.yaml&#x000A;NAME            STATUS   AGE&#x000A;namespace/dev   Active   18s&#x000A;&#x000A;NAME            READY   STATUS    RESTARTS   AGE&#x000A;pod/nginxpod    1/1     Running   0          17s&#x000A;```&#x000A;&#x000A;这样就显示了两个资源对象的信息&#x000A;&#x000A;4）执行delete命令，删除资源：&#x000A;&#x000A;```shell&#x000A;[root@master ~]# kubectl delete -f nginxpod.yaml&#x000A;namespace &quot;dev&quot; deleted&#x000A;pod &quot;nginxpod&quot; deleted&#x000A;```&#x000A;&#x000A;此时发现两个资源对象被删除了&#x000A;&#x000A;```&#x000A;总结:&#x000A;    命令式对象配置的方式操作资源，可以简单的认为：命令  +  yaml配置文件（里面是命令需要的各种参数）&#x000A;```&#x000A;&#x000A;### 3.3.3 声明式对象配置&#x000A;&#x000A;声明式对象配置跟命令式对象配置很相似，但是它只有一个命令apply。&#x000A;&#x000A;```shell&#x000A;# 首先执行一次kubectl apply -f yaml文件，发现创建了资源&#x000A;[root@master ~]#  kubectl apply -f nginxpod.yaml&#x000A;namespace/dev created&#x000A;pod/nginxpod created&#x000A;&#x000A;# 再次执行一次kubectl apply -f yaml文件，发现说资源没有变动&#x000A;[root@master ~]#  kubectl apply -f nginxpod.yaml&#x000A;namespace/dev unchanged&#x000A;pod/nginxpod unchanged&#x000A;```&#x000A;&#x000A;```powershell&#x000A;总结:&#x000A;    其实声明式对象配置就是使用apply描述一个资源最终的状态（在yaml中定义状态）&#x000A;    使用apply操作资源：&#x000A;        如果资源不存在，就创建，相当于 kubectl create&#x000A;        如果资源已存在，就更新，相当于 kubectl patch&#x000A;```&#x000A;&#x000A;&gt; 扩展：kubectl可以在node节点上运行吗 ?&#x000A;&#x000A;kubectl的运行是需要进行配置的，它的配置文件是$HOME/.kube，如果想要在node节点运行此命令，需要将master上的.kube文件复制到node节点上，即在master节点上执行下面操作：&#x000A;&#x000A;```shell&#x000A;scp  -r  HOME/.kube   node1: HOME/&#x000A;```&#x000A;&#x000A;&gt; 使用推荐: 三种方式应该怎么用 ?&#x000A;&#x000A;创建/更新资源 使用声明式对象配置 kubectl apply -f XXX.yaml&#x000A;&#x000A;删除资源 使用命令式对象配置 kubectl delete -f XXX.yaml&#x000A;&#x000A;查询资源 使用命令式对象管理 kubectl get(describe) 资源名称&#x000A;&#x000A;### 4. 实战入门&#x000A;&#x000A;本章节将介绍如何在kubernetes集群中部署一个nginx服务，并且能够对其进行访问。&#x000A;&#x000A;#### 4.1 Namespace&#x000A;&#x000A;Namespace是kubernetes系统中的一种非常重要资源，它的主要作用是用来实现**多套环境的资源隔离**或者**多租户的资源隔离**。&#x000A;&#x000A;默认情况下，kubernetes集群中的所有的Pod都是可以相互访问的。但是在实际中，可能不想让两个Pod之间进行互相的访问，那此时就可以将两个Pod划分到不同的namespace下。kubernetes通过将集群内部的资源分配到不同的Namespace中，可以形成逻辑上的&quot;组&quot;，以方便不同的组的资源进行隔离使用和管理。&#x000A;&#x000A;可以通过kubernetes的授权机制，将不同的namespace交给不同租户进行管理，这样就实现了多租户的资源隔离。此时还能结合kubernetes的资源配额机制，限定不同租户能占用的资源，例如CPU使用量、内存使用量等等，来实现租户可用资源的管理。&#x000A;&#x000A;![image-20200407100850484](Kubenetes.assets/image-20200407100850484.png)&#x000A;&#x000A;kubernetes在集群启动之后，会默认创建几个namespace&#x000A;&#x000A;&#x000A;&#x000A;```shell&#x000A;[root@master ~]# kubectl  get namespace&#x000A;NAME              STATUS   AGE&#x000A;default           Active   45h     #  所有未指定Namespace的对象都会被分配在default命名空间&#x000A;kube-node-lease   Active   45h     #  集群节点之间的心跳维护，v1.13开始引入&#x000A;kube-public       Active   45h     #  此命名空间下的资源可以被所有人访问（包括未认证用户）&#x000A;kube-system       Active   45h     #  所有由Kubernetes系统创建的资源都处于这个命名空间&#x000A;```&#x000A;&#x000A;下面来看namespace资源的具体操作：&#x000A;&#x000A;##### 4.1.1 **查看**&#x000A;&#x000A;```shell&#x000A;# 1 查看所有的ns  命令：kubectl get ns&#x000A;[root@master ~]# kubectl get ns&#x000A;NAME              STATUS   AGE&#x000A;default           Active   45h&#x000A;kube-node-lease   Active   45h&#x000A;kube-public       Active   45h     &#x000A;kube-system       Active   45h     &#x000A;&#x000A;# 2 查看指定的ns   命令：kubectl get ns ns名称&#x000A;[root@master ~]# kubectl get ns default&#x000A;NAME      STATUS   AGE&#x000A;default   Active   45h&#x000A;&#x000A;# 3 指定输出格式  命令：kubectl get ns ns名称  -o 格式参数&#x000A;# kubernetes支持的格式有很多，比较常见的是wide、json、yaml&#x000A;[root@master ~]# kubectl get ns default -o yaml&#x000A;apiVersion: v1&#x000A;kind: Namespace&#x000A;metadata:&#x000A;  creationTimestamp: &quot;2021-05-08T04:44:16Z&quot;&#x000A;  name: default&#x000A;  resourceVersion: &quot;151&quot;&#x000A;  selfLink: /api/v1/namespaces/default&#x000A;  uid: 7405f73a-e486-43d4-9db6-145f1409f090&#x000A;spec:&#x000A;  finalizers:&#x000A;  - kubernetes&#x000A;status:&#x000A;  phase: Active&#x000A;  &#x000A;# 4 查看ns详情  命令：kubectl describe ns ns名称&#x000A;[root@master ~]# kubectl describe ns default&#x000A;Name:         default&#x000A;Labels:       &lt;none&gt;&#x000A;Annotations:  &lt;none&gt;&#x000A;Status:       Active  # Active 命名空间正在使用中  Terminating 正在删除命名空间&#x000A;&#x000A;# ResourceQuota 针对namespace做的资源限制&#x000A;# LimitRange针对namespace中的每个组件做的资源限制&#x000A;No resource quota.&#x000A;No LimitRange resource.&#x000A;```&#x000A;&#x000A;##### 4.1.2 **创建**&#x000A;&#x000A;```shell&#x000A;# 创建namespace&#x000A;[root@master ~]# kubectl create ns dev&#x000A;namespace/dev created&#x000A;```&#x000A;&#x000A;##### 4.1.3 **删除**&#x000A;&#x000A;```shell&#x000A;# 删除namespace&#x000A;[root@master ~]# kubectl delete ns dev&#x000A;namespace &quot;dev&quot; deleted&#x000A;```&#x000A;&#x000A;##### 4.1.4 **配置方式**&#x000A;&#x000A;首先准备一个yaml文件：ns-dev.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Namespace&#x000A;metadata:&#x000A;  name: dev&#x000A;```&#x000A;&#x000A;然后就可以执行对应的创建和删除命令了：&#x000A;&#x000A;创建：kubectl create -f ns-dev.yaml&#x000A;&#x000A;删除：kubectl delete -f ns-dev.yaml&#x000A;&#x000A;#### 4.2 Pod&#x000A;&#x000A;Pod是kubernetes集群进行管理的最小单元，程序要运行必须部署在容器中，而容器必须存在于Pod中。&#x000A;&#x000A;Pod可以认为是容器的封装，一个Pod中可以存在一个或者多个容器。&#x000A;&#x000A;![image-20200407121501907](Kubenetes.assets/image-20200407121501907.png)&#x000A;&#x000A;kubernetes在集群启动之后，集群中的各个组件也都是以Pod方式运行的。可以通过下面命令查看：&#x000A;&#x000A;```shell&#x000A;[root@master ~]# kubectl get pod -n kube-system&#x000A;NAMESPACE     NAME                             READY   STATUS    RESTARTS   AGE&#x000A;kube-system   coredns-6955765f44-68g6v         1/1     Running   0          2d1h&#x000A;kube-system   coredns-6955765f44-cs5r8         1/1     Running   0          2d1h&#x000A;kube-system   etcd-master                      1/1     Running   0          2d1h&#x000A;kube-system   kube-apiserver-master            1/1     Running   0          2d1h&#x000A;kube-system   kube-controller-manager-master   1/1     Running   0          2d1h&#x000A;kube-system   kube-flannel-ds-amd64-47r25      1/1     Running   0          2d1h&#x000A;kube-system   kube-flannel-ds-amd64-ls5lh      1/1     Running   0          2d1h&#x000A;kube-system   kube-proxy-685tk                 1/1     Running   0          2d1h&#x000A;kube-system   kube-proxy-87spt                 1/1     Running   0          2d1h&#x000A;kube-system   kube-scheduler-master            1/1     Running   0          2d1h&#x000A;```&#x000A;&#x000A;##### 4.2.1 创建并运行&#x000A;&#x000A;kubernetes没有提供单独运行Pod的命令，都是通过Pod控制器来实现的&#x000A;&#x000A;```shell&#x000A;# 命令格式： kubectl run (pod控制器名称) [参数] &#x000A;# --image  指定Pod的镜像&#x000A;# --port   指定端口&#x000A;# --namespace  指定namespace&#x000A;[root@master ~]# kubectl run nginx --image=nginx:latest --port=80 --namespace dev &#x000A;deployment.apps/nginx created&#x000A;```&#x000A;&#x000A;##### 4.2.2 查看pod信息&#x000A;&#x000A;```shell&#x000A;# 查看Pod基本信息&#x000A;[root@master ~]# kubectl get pods -n dev&#x000A;NAME    READY   STATUS    RESTARTS   AGE&#x000A;nginx   1/1     Running   0          43s&#x000A;&#x000A;# 查看Pod的详细信息&#x000A;[root@master ~]# kubectl describe pod nginx -n dev&#x000A;Name:         nginx&#x000A;Namespace:    dev&#x000A;Priority:     0&#x000A;Node:         node1/192.168.5.4&#x000A;Start Time:   Wed, 08 May 2021 09:29:24 +0800&#x000A;Labels:       pod-template-hash=5ff7956ff6&#x000A;              run=nginx&#x000A;Annotations:  &lt;none&gt;&#x000A;Status:       Running&#x000A;IP:           10.244.1.23&#x000A;IPs:&#x000A;  IP:           10.244.1.23&#x000A;Controlled By:  ReplicaSet/nginx&#x000A;Containers:&#x000A;  nginx:&#x000A;    Container ID:   docker://4c62b8c0648d2512380f4ffa5da2c99d16e05634979973449c98e9b829f6253c&#x000A;    Image:          nginx:latest&#x000A;    Image ID:       docker-pullable://nginx@sha256:485b610fefec7ff6c463ced9623314a04ed67e3945b9c08d7e53a47f6d108dc7&#x000A;    Port:           80/TCP&#x000A;    Host Port:      0/TCP&#x000A;    State:          Running&#x000A;      Started:      Wed, 08 May 2021 09:30:01 +0800&#x000A;    Ready:          True&#x000A;    Restart Count:  0&#x000A;    Environment:    &lt;none&gt;&#x000A;    Mounts:&#x000A;      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hwvvw (ro)&#x000A;Conditions:&#x000A;  Type              Status&#x000A;  Initialized       True&#x000A;  Ready             True&#x000A;  ContainersReady   True&#x000A;  PodScheduled      True&#x000A;Volumes:&#x000A;  default-token-hwvvw:&#x000A;    Type:        Secret (a volume populated by a Secret)&#x000A;    SecretName:  default-token-hwvvw&#x000A;    Optional:    false&#x000A;QoS Class:       BestEffort&#x000A;Node-Selectors:  &lt;none&gt;&#x000A;Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s&#x000A;                 node.kubernetes.io/unreachable:NoExecute for 300s&#x000A;Events:&#x000A;  Type    Reason     Age        From               Message&#x000A;  ----    ------     ----       ----               -------&#x000A;  Normal  Scheduled  &lt;unknown&gt;  default-scheduler  Successfully assigned dev/nginx-5ff7956ff6-fg2db to node1&#x000A;  Normal  Pulling    4m11s      kubelet, node1     Pulling image &quot;nginx:latest&quot;&#x000A;  Normal  Pulled     3m36s      kubelet, node1     Successfully pulled image &quot;nginx:latest&quot;&#x000A;  Normal  Created    3m36s      kubelet, node1     Created container nginx&#x000A;  Normal  Started    3m36s      kubelet, node1     Started container nginx&#x000A;```&#x000A;&#x000A;##### 4.2.3 访问Pod&#x000A;&#x000A;```shell&#x000A;# 获取podIP&#x000A;[root@master ~]# kubectl get pods -n dev -o wide&#x000A;NAME    READY   STATUS    RESTARTS   AGE    IP             NODE    ... &#x000A;nginx   1/1     Running   0          190s   10.244.1.23   node1   ...&#x000A;&#x000A;#访问POD&#x000A;[root@master ~]# curl http://10.244.1.23:80&#x000A;&lt;!DOCTYPE html&gt;&#x000A;&lt;html&gt;&#x000A;&lt;head&gt;&#x000A;	&lt;title&gt;Welcome to nginx!&lt;/title&gt;&#x000A;&lt;/head&gt;&#x000A;&lt;body&gt;&#x000A;	&lt;p&gt;&lt;em&gt;Thank you for using nginx.&lt;/em&gt;&lt;/p&gt;&#x000A;&lt;/body&gt;&#x000A;&lt;/html&gt;&#x000A;```&#x000A;&#x000A;##### 4.2.4 删除指定Pod&#x000A;&#x000A;```shell&#x000A;# 删除指定Pod&#x000A;[root@master ~]# kubectl delete pod nginx -n dev&#x000A;pod &quot;nginx&quot; deleted&#x000A;&#x000A;# 此时，显示删除Pod成功，但是再查询，发现又新产生了一个 &#x000A;[root@master ~]# kubectl get pods -n dev&#x000A;NAME    READY   STATUS    RESTARTS   AGE&#x000A;nginx   1/1     Running   0          21s&#x000A;&#x000A;# 这是因为当前Pod是由Pod控制器创建的，控制器会监控Pod状况，一旦发现Pod死亡，会立即重建&#x000A;# 此时要想删除Pod，必须删除Pod控制器&#x000A;&#x000A;# 先来查询一下当前namespace下的Pod控制器&#x000A;[root@master ~]# kubectl get deploy -n  dev&#x000A;NAME    READY   UP-TO-DATE   AVAILABLE   AGE&#x000A;nginx   1/1     1            1           9m7s&#x000A;&#x000A;# 接下来，删除此PodPod控制器&#x000A;[root@master ~]# kubectl delete deploy nginx -n dev&#x000A;deployment.apps &quot;nginx&quot; deleted&#x000A;&#x000A;# 稍等片刻，再查询Pod，发现Pod被删除了&#x000A;[root@master ~]# kubectl get pods -n dev&#x000A;No resources found in dev namespace.&#x000A;```&#x000A;&#x000A;##### 4.2.5 配置操作&#x000A;&#x000A;创建一个pod-nginx.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: nginx&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - image: nginx:latest&#x000A;    name: pod&#x000A;    ports:&#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;      protocol: TCP&#x000A;```&#x000A;&#x000A;然后就可以执行对应的创建和删除命令了：&#x000A;&#x000A;创建：kubectl create -f pod-nginx.yaml&#x000A;&#x000A;删除：kubectl delete -f pod-nginx.yaml&#x000A;&#x000A;#### 4.3 Label&#x000A;&#x000A;Label是kubernetes系统中的一个重要概念。它的作用就是在资源上添加标识，用来对它们进行区分和选择。&#x000A;&#x000A;Label的特点：&#x000A;&#x000A;- 一个Label会以key/value键值对的形式附加到各种对象上，如Node、Pod、Service等等&#x000A;- 一个资源对象可以定义任意数量的Label ，同一个Label也可以被添加到任意数量的资源对象上去&#x000A;- Label通常在资源对象定义时确定，当然也可以在对象创建后动态添加或者删除&#x000A;&#x000A;可以通过Label实现资源的多维度分组，以便灵活、方便地进行资源分配、调度、配置、部署等管理工作。&#x000A;&#x000A;&gt; 一些常用的Label 示例如下：&#x000A;&gt;&#x000A;&gt; - 版本标签：&quot;version&quot;:&quot;release&quot;, &quot;version&quot;:&quot;stable&quot;......&#x000A;&gt; - 环境标签：&quot;environment&quot;:&quot;dev&quot;，&quot;environment&quot;:&quot;test&quot;，&quot;environment&quot;:&quot;pro&quot;&#x000A;&gt; - 架构标签：&quot;tier&quot;:&quot;frontend&quot;，&quot;tier&quot;:&quot;backend&quot;&#x000A;&#x000A;标签定义完毕之后，还要考虑到标签的选择，这就要使用到Label Selector，即：&#x000A;&#x000A;Label用于给某个资源对象定义标识&#x000A;&#x000A;Label Selector用于查询和筛选拥有某些标签的资源对象&#x000A;&#x000A;当前有两种Label Selector：&#x000A;&#x000A;- 基于等式的Label Selector&#x000A;&#x000A;  name = slave: 选择所有包含Label中key=&quot;name&quot;且value=&quot;slave&quot;的对象&#x000A;&#x000A;  env != production: 选择所有包括Label中的key=&quot;env&quot;且value不等于&quot;production&quot;的对象&#x000A;&#x000A;- 基于集合的Label Selector&#x000A;&#x000A;  name in (master, slave): 选择所有包含Label中的key=&quot;name&quot;且value=&quot;master&quot;或&quot;slave&quot;的对象&#x000A;&#x000A;  name not in (frontend): 选择所有包含Label中的key=&quot;name&quot;且value不等于&quot;frontend&quot;的对象&#x000A;&#x000A;标签的选择条件可以使用多个，此时将多个Label Selector进行组合，使用逗号&quot;,&quot;进行分隔即可。例如：&#x000A;&#x000A;name=slave，env!=production&#x000A;&#x000A;name not in (frontend)，env!=production&#x000A;&#x000A;##### 4.3.1 命令方式&#x000A;&#x000A;```shell&#x000A;# 为pod资源打标签&#x000A;[root@master ~]# kubectl label pod nginx-pod version=1.0 -n dev&#x000A;pod/nginx-pod labeled&#x000A;&#x000A;# 为pod资源更新标签&#x000A;[root@master ~]# kubectl label pod nginx-pod version=2.0 -n dev --overwrite&#x000A;pod/nginx-pod labeled&#x000A;&#x000A;# 查看标签&#x000A;[root@master ~]# kubectl get pod nginx-pod  -n dev --show-labels&#x000A;NAME        READY   STATUS    RESTARTS   AGE   LABELS&#x000A;nginx-pod   1/1     Running   0          10m   version=2.0&#x000A;&#x000A;# 筛选标签&#x000A;[root@master ~]# kubectl get pod -n dev -l version=2.0  --show-labels&#x000A;NAME        READY   STATUS    RESTARTS   AGE   LABELS&#x000A;nginx-pod   1/1     Running   0          17m   version=2.0&#x000A;[root@master ~]# kubectl get pod -n dev -l version!=2.0 --show-labels&#x000A;No resources found in dev namespace.&#x000A;&#x000A;#删除标签&#x000A;[root@master ~]# kubectl label pod nginx-pod -n dev tier-&#x000A;pod/nginx unlabeled&#x000A;```&#x000A;&#x000A;##### 4.3.2 配置方式&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: nginx&#x000A;  namespace: dev&#x000A;  labels:&#x000A;    version: &quot;3.0&quot; &#x000A;    env: &quot;test&quot;&#x000A;spec:&#x000A;  containers:&#x000A;  - image: nginx:latest&#x000A;    name: pod&#x000A;    ports:&#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;      protocol: TCP&#x000A;```&#x000A;&#x000A;然后就可以执行对应的更新命令了：kubectl apply -f pod-nginx.yaml&#x000A;&#x000A;#### 4.4 Deployment&#x000A;&#x000A;在kubernetes中，Pod是最小的控制单元，但是kubernetes很少直接控制Pod，一般都是通过Pod控制器来完成的。Pod控制器用于pod的管理，确保pod资源符合预期的状态，当pod的资源出现故障时，会尝试进行重启或重建pod。&#x000A;&#x000A;在kubernetes中Pod控制器的种类有很多，本章节只介绍一种：Deployment。&#x000A;&#x000A;![image-20200408193950807](Kubenetes.assets/image-20200408193950807.png)&#x000A;&#x000A;##### 4.4.1 命令操作&#x000A;&#x000A;```shell&#x000A;# 命令格式: kubectl create deployment 名称  [参数] &#x000A;# --image  指定pod的镜像&#x000A;# --port   指定端口&#x000A;# --replicas  指定创建pod数量&#x000A;# --namespace  指定namespace&#x000A;[root@master ~]# kubectl run nginx --image=nginx:latest --port=80 --replicas=3 -n dev&#x000A;deployment.apps/nginx created&#x000A;&#x000A;# 查看创建的Pod&#x000A;[root@master ~]# kubectl get pods -n dev&#x000A;NAME                     READY   STATUS    RESTARTS   AGE&#x000A;nginx-5ff7956ff6-6k8cb   1/1     Running   0          19s&#x000A;nginx-5ff7956ff6-jxfjt   1/1     Running   0          19s&#x000A;nginx-5ff7956ff6-v6jqw   1/1     Running   0          19s&#x000A;&#x000A;# 查看deployment的信息&#x000A;[root@master ~]# kubectl get deploy -n dev&#x000A;NAME    READY   UP-TO-DATE   AVAILABLE   AGE&#x000A;nginx   3/3     3            3           2m42s&#x000A;&#x000A;# UP-TO-DATE：成功升级的副本数量&#x000A;# AVAILABLE：可用副本的数量&#x000A;[root@master ~]# kubectl get deploy -n dev -o wide&#x000A;NAME    READY UP-TO-DATE  AVAILABLE   AGE     CONTAINERS   IMAGES              SELECTOR&#x000A;nginx   3/3     3         3           2m51s   nginx        nginx:latest        run=nginx&#x000A;&#x000A;# 查看deployment的详细信息&#x000A;[root@master ~]# kubectl describe deploy nginx -n dev&#x000A;Name:                   nginx&#x000A;Namespace:              dev&#x000A;CreationTimestamp:      Wed, 08 May 2021 11:14:14 +0800&#x000A;Labels:                 run=nginx&#x000A;Annotations:            deployment.kubernetes.io/revision: 1&#x000A;Selector:               run=nginx&#x000A;Replicas:               3 desired | 3 updated | 3 total | 3 available | 0 unavailable&#x000A;StrategyType:           RollingUpdate&#x000A;MinReadySeconds:        0&#x000A;RollingUpdateStrategy:  25% max unavailable, 25% max 违规词汇&#x000A;Pod Template:&#x000A;  Labels:  run=nginx&#x000A;  Containers:&#x000A;   nginx:&#x000A;    Image:        nginx:latest&#x000A;    Port:         80/TCP&#x000A;    Host Port:    0/TCP&#x000A;    Environment:  &lt;none&gt;&#x000A;    Mounts:       &lt;none&gt;&#x000A;  Volumes:        &lt;none&gt;&#x000A;Conditions:&#x000A;  Type           Status  Reason&#x000A;  ----           ------  ------&#x000A;  Available      True    MinimumReplicasAvailable&#x000A;  Progressing    True    NewReplicaSetAvailable&#x000A;OldReplicaSets:  &lt;none&gt;&#x000A;NewReplicaSet:   nginx-5ff7956ff6 (3/3 replicas created)&#x000A;Events:&#x000A;  Type    Reason             Age    From                   Message&#x000A;  ----    ------             ----   ----                   -------&#x000A;  Normal  ScalingReplicaSet  5m43s  deployment-controller  Scaled up replicaset nginx-5ff7956ff6 to 3&#x000A;  &#x000A;# 删除 &#x000A;[root@master ~]# kubectl delete deploy nginx -n dev&#x000A;deployment.apps &quot;nginx&quot; deleted&#x000A;```&#x000A;&#x000A;##### 4.4.2 配置操作&#x000A;&#x000A;创建一个deploy-nginx.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1&#x000A;kind: Deployment&#x000A;metadata:&#x000A;  name: nginx&#x000A;  namespace: dev&#x000A;spec:&#x000A;  replicas: 3&#x000A;  selector:&#x000A;    matchLabels:&#x000A;      run: nginx&#x000A;  template:&#x000A;    metadata:&#x000A;      labels:&#x000A;        run: nginx&#x000A;    spec:&#x000A;      containers:&#x000A;      - image: nginx:latest&#x000A;        name: nginx&#x000A;        ports:&#x000A;        - containerPort: 80&#x000A;          protocol: TCP&#x000A;```&#x000A;&#x000A;然后就可以执行对应的创建和删除命令了：&#x000A;&#x000A;创建：kubectl create -f deploy-nginx.yaml&#x000A;&#x000A;删除：kubectl delete -f deploy-nginx.yaml&#x000A;&#x000A;#### 4.5 Service&#x000A;&#x000A;通过上节课的学习，已经能够利用Deployment来创建一组Pod来提供具有高可用性的服务。&#x000A;&#x000A;虽然每个Pod都会分配一个单独的Pod IP，然而却存在如下两问题：&#x000A;&#x000A;- Pod IP 会随着Pod的重建产生变化&#x000A;- Pod IP 仅仅是集群内可见的虚拟IP，外部无法访问&#x000A;&#x000A;这样对于访问这个服务带来了难度。因此，kubernetes设计了Service来解决这个问题。&#x000A;&#x000A;Service可以看作是一组同类Pod**对外的访问接口**。借助Service，应用可以方便地实现服务发现和负载均衡。&#x000A;&#x000A;![image-20200408194716912](Kubenetes.assets/image-20200408194716912.png)&#x000A;&#x000A;##### 4.5.1 创建集群内部可访问的Service&#x000A;&#x000A;```shell&#x000A;# 暴露Service&#x000A;[root@master ~]# kubectl expose deploy nginx --name=svc-nginx1 --type=ClusterIP --port=80 --target-port=80 -n dev&#x000A;service/svc-nginx1 exposed&#x000A;&#x000A;# 查看service&#x000A;[root@master ~]# kubectl get svc svc-nginx1 -n dev -o wide&#x000A;NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE     SELECTOR&#x000A;svc-nginx1   ClusterIP   10.109.179.231   &lt;none&gt;        80/TCP    3m51s   run=nginx&#x000A;&#x000A;# 这里产生了一个CLUSTER-IP，这就是service的IP，在Service的生命周期中，这个地址是不会变动的&#x000A;# 可以通过这个IP访问当前service对应的POD&#x000A;[root@master ~]# curl 10.109.179.231:80&#x000A;&lt;!DOCTYPE html&gt;&#x000A;&lt;html&gt;&#x000A;&lt;head&gt;&#x000A;&lt;title&gt;Welcome to nginx!&lt;/title&gt;&#x000A;&lt;/head&gt;&#x000A;&lt;body&gt;&#x000A;&lt;h1&gt;Welcome to nginx!&lt;/h1&gt;&#x000A;.......&#x000A;&lt;/body&gt;&#x000A;&lt;/html&gt;&#x000A;```&#x000A;&#x000A;##### 4.5.2 创建集群外部也可访问的Service&#x000A;&#x000A;```shell&#x000A;# 上面创建的Service的type类型为ClusterIP，这个ip地址只用集群内部可访问&#x000A;# 如果需要创建外部也可以访问的Service，需要修改type为NodePort&#x000A;[root@master ~]# kubectl expose deploy nginx --name=svc-nginx2 --type=NodePort --port=80 --target-port=80 -n dev&#x000A;service/svc-nginx2 exposed&#x000A;&#x000A;# 此时查看，会发现出现了NodePort类型的Service，而且有一对Port（80:31928/TC）&#x000A;[root@master ~]# kubectl get svc  svc-nginx2  -n dev -o wide&#x000A;NAME          TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE    SELECTOR&#x000A;svc-nginx2    NodePort    10.100.94.0      &lt;none&gt;        80:31928/TCP   9s     run=nginx&#x000A;&#x000A;# 接下来就可以通过集群外的主机访问 节点IP:31928访问服务了&#x000A;# 例如在的电脑主机上通过浏览器访问下面的地址&#x000A;http://192.168.90.100:31928/&#x000A;```&#x000A;&#x000A;##### 4.5.3 删除Service&#x000A;&#x000A;```shell&#x000A;[root@master ~]# kubectl delete svc svc-nginx-1 -n dev &#x000A;service &quot;svc-nginx-1&quot; deleted&#x000A;```&#x000A;&#x000A;##### 4.5.4 配置方式&#x000A;&#x000A;创建一个svc-nginx.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Service&#x000A;metadata:&#x000A;  name: svc-nginx&#x000A;  namespace: dev&#x000A;spec:&#x000A;  clusterIP: 10.109.179.231 #固定svc的内网ip&#x000A;  ports:&#x000A;  - port: 80&#x000A;    protocol: TCP&#x000A;    targetPort: 80&#x000A;  selector:&#x000A;    run: nginx&#x000A;  type: ClusterIP&#x000A;```&#x000A;&#x000A;然后就可以执行对应的创建和删除命令了：&#x000A;&#x000A;创建：kubectl create -f svc-nginx.yaml&#x000A;&#x000A;删除：kubectl delete -f svc-nginx.yaml&#x000A;&#x000A;&gt; **小结**&#x000A;&gt;&#x000A;&gt; 至此，已经掌握了Namespace、Pod、Deployment、Service资源的基本操作，有了这些操作，就可以在kubernetes集群中实现一个服务的简单部署和访问了，但是如果想要更好的使用kubernetes，就需要深入学习这几种资源的细节和原理。&#x000A;&#x000A;### 5. Pod详解&#x000A;&#x000A;#### 5.1 Pod介绍&#x000A;&#x000A;##### 5.1.1 Pod结构&#x000A;&#x000A;![image-20200407121501907](Kubenetes.assets/image-20200407121501907-1626781151898.png)&#x000A;&#x000A;每个Pod中都可以包含一个或者多个容器，这些容器可以分为两类：&#x000A;&#x000A;- 用户程序所在的容器，数量可多可少&#x000A;&#x000A;- Pause容器，这是每个Pod都会有的一个**根容器**，它的作用有两个：&#x000A;&#x000A;  - 可以以它为依据，评估整个Pod的健康状态&#x000A;&#x000A;  - 可以在根容器上设置Ip地址，其它容器都此Ip（Pod IP），以实现Pod内部的网路通信&#x000A;&#x000A;    ```&#x000A;    这里是Pod内部的通讯，Pod的之间的通讯采用虚拟二层网络技术来实现，我们当前环境用的是Flannel&#x000A;    ```&#x000A;&#x000A;##### 5.1.2 Pod定义&#x000A;&#x000A;下面是Pod的资源清单：&#x000A;&#x000A;```shell&#x000A;apiVersion: v1     #必选，版本号，例如v1&#x000A;kind: Pod       　 #必选，资源类型，例如 Pod&#x000A;metadata:       　 #必选，元数据&#x000A;  name: string     #必选，Pod名称&#x000A;  namespace: string  #Pod所属的命名空间,默认为&quot;default&quot;&#x000A;  labels:       　　  #自定义标签列表&#x000A;    - name: string      　          &#x000A;spec:  #必选，Pod中容器的详细定义&#x000A;  containers:  #必选，Pod中容器列表&#x000A;  - name: string   #必选，容器名称&#x000A;    image: string  #必选，容器的镜像名称&#x000A;    imagePullPolicy: [ Always|Never|IfNotPresent ]  #获取镜像的策略 &#x000A;    command: [string]   #容器的启动命令列表，如不指定，使用打包时使用的启动命令&#x000A;    args: [string]      #容器的启动命令参数列表&#x000A;    workingDir: string  #容器的工作目录&#x000A;    volumeMounts:       #挂载到容器内部的存储卷配置&#x000A;    - name: string      #引用pod定义的共享存储卷的名称，需用volumes[]部分定义的的卷名&#x000A;      mountPath: string #存储卷在容器内mount的绝对路径，应少于512字符&#x000A;      readOnly: boolean #是否为只读模式&#x000A;    ports: #需要暴露的端口库号列表&#x000A;    - name: string        #端口的名称&#x000A;      containerPort: int  #容器需要监听的端口号&#x000A;      hostPort: int       #容器所在主机需要监听的端口号，默认与Container相同&#x000A;      protocol: string    #端口协议，支持TCP和UDP，默认TCP&#x000A;    env:   #容器运行前需设置的环境变量列表&#x000A;    - name: string  #环境变量名称&#x000A;      value: string #环境变量的值&#x000A;    resources: #资源限制和请求的设置&#x000A;      limits:  #资源限制的设置&#x000A;        cpu: string     #Cpu的限制，单位为core数，将用于docker run --cpu-shares参数&#x000A;        memory: string  #内存限制，单位可以为Mib/Gib，将用于docker run --memory参数&#x000A;      requests: #资源请求的设置&#x000A;        cpu: string    #Cpu请求，容器启动的初始可用数量&#x000A;        memory: string #内存请求,容器启动的初始可用数量&#x000A;    lifecycle: #生命周期钩子&#x000A;        postStart: #容器启动后立即执行此钩子,如果执行失败,会根据重启策略进行重启&#x000A;        preStop: #容器终止前执行此钩子,无论结果如何,容器都会终止&#x000A;    livenessProbe:  #对Pod内各容器健康检查的设置，当探测无响应几次后将自动重启该容器&#x000A;      exec:       　 #对Pod容器内检查方式设置为exec方式&#x000A;        command: [string]  #exec方式需要制定的命令或脚本&#x000A;      httpGet:       #对Pod内个容器健康检查方法设置为HttpGet，需要制定Path、port&#x000A;        path: string&#x000A;        port: number&#x000A;        host: string&#x000A;        scheme: string&#x000A;        HttpHeaders:&#x000A;        - name: string&#x000A;          value: string&#x000A;      tcpSocket:     #对Pod内个容器健康检查方式设置为tcpSocket方式&#x000A;         port: number&#x000A;       initialDelaySeconds: 0       #容器启动完成后首次探测的时间，单位为秒&#x000A;       timeoutSeconds: 0    　　    #对容器健康检查探测等待响应的超时时间，单位秒，默认1秒&#x000A;       periodSeconds: 0     　　    #对容器监控检查的定期探测时间设置，单位秒，默认10秒一次&#x000A;       successThreshold: 0&#x000A;       failureThreshold: 0&#x000A;       securityContext:&#x000A;         privileged: false&#x000A;  restartPolicy: [Always | Never | OnFailure]  #Pod的重启策略&#x000A;  nodeName: &lt;string&gt; #设置NodeName表示将该Pod调度到指定到名称的node节点上&#x000A;  nodeSelector: obeject #设置NodeSelector表示将该Pod调度到包含这个label的node上&#x000A;  imagePullSecrets: #Pull镜像时使用的secret名称，以key：secretkey格式指定&#x000A;  - name: string&#x000A;  hostNetwork: false   #是否使用主机网络模式，默认为false，如果设置为true，表示使用宿主机网络&#x000A;  volumes:   #在该pod上定义共享存储卷列表&#x000A;  - name: string    #共享存储卷名称 （volumes类型有很多种）&#x000A;    emptyDir: {}       #类型为emtyDir的存储卷，与Pod同生命周期的一个临时目录。为空值&#x000A;    hostPath: string   #类型为hostPath的存储卷，表示挂载Pod所在宿主机的目录&#x000A;      path: string      　　        #Pod所在宿主机的目录，将被用于同期中mount的目录&#x000A;    secret:       　　　#类型为secret的存储卷，挂载集群与定义的secret对象到容器内部&#x000A;      scretname: string  &#x000A;      items:     &#x000A;      - key: string&#x000A;        path: string&#x000A;    configMap:         #类型为configMap的存储卷，挂载预定义的configMap对象到容器内部&#x000A;      name: string&#x000A;      items:&#x000A;      - key: string&#x000A;        path: string&#x000A;```&#x000A;&#x000A;```shell&#x000A;#小提示：&#x000A;#   在这里，可通过一个命令来查看每种资源的可配置项&#x000A;#   kubectl explain 资源类型         查看某种资源可以配置的一级属性&#x000A;#   kubectl explain 资源类型.属性     查看属性的子属性&#x000A;[root@k8s-master01 ~]# kubectl explain pod&#x000A;KIND:     Pod&#x000A;VERSION:  v1&#x000A;FIELDS:&#x000A;   apiVersion   &lt;string&gt;&#x000A;   kind &lt;string&gt;&#x000A;   metadata     &lt;Object&gt;&#x000A;   spec &lt;Object&gt;&#x000A;   status       &lt;Object&gt;&#x000A;&#x000A;[root@k8s-master01 ~]# kubectl explain pod.metadata&#x000A;KIND:     Pod&#x000A;VERSION:  v1&#x000A;RESOURCE: metadata &lt;Object&gt;&#x000A;FIELDS:&#x000A;   annotations  &lt;map[string]string&gt;&#x000A;   clusterName  &lt;string&gt;&#x000A;   creationTimestamp    &lt;string&gt;&#x000A;   deletionGracePeriodSeconds   &lt;integer&gt;&#x000A;   deletionTimestamp    &lt;string&gt;&#x000A;   finalizers   &lt;[]string&gt;&#x000A;   generateName &lt;string&gt;&#x000A;   generation   &lt;integer&gt;&#x000A;   labels       &lt;map[string]string&gt;&#x000A;   managedFields        &lt;[]Object&gt;&#x000A;   name &lt;string&gt;&#x000A;   namespace    &lt;string&gt;&#x000A;   ownerReferences      &lt;[]Object&gt;&#x000A;   resourceVersion      &lt;string&gt;&#x000A;   selfLink     &lt;string&gt;&#x000A;   uid  &lt;string&gt;&#x000A;```&#x000A;&#x000A;在kubernetes中基本所有资源的一级属性都是一样的，主要包含5部分：&#x000A;&#x000A;- apiVersion &lt;string&gt; 版本，由kubernetes内部定义，版本号必须可以用 kubectl api-versions 查询到&#x000A;- kind &lt;string&gt; 类型，由kubernetes内部定义，版本号必须可以用 kubectl api-resources 查询到&#x000A;- metadata &lt;Object&gt; 元数据，主要是资源标识和说明，常用的有name、namespace、labels等&#x000A;- spec &lt;Object&gt; 描述，这是配置中最重要的一部分，里面是对各种资源配置的详细描述&#x000A;- status &lt;Object&gt; 状态信息，里面的内容不需要定义，由kubernetes自动生成&#x000A;&#x000A;在上面的属性中，spec是接下来研究的重点，继续看下它的常见子属性:&#x000A;&#x000A;- containers &lt;[]Object&gt; 容器列表，用于定义容器的详细信息&#x000A;- nodeName &lt;String&gt; 根据nodeName的值将pod调度到指定的Node节点上&#x000A;- nodeSelector &lt;map[]&gt; 根据NodeSelector中定义的信息选择将该Pod调度到包含这些label的Node 上&#x000A;- hostNetwork &lt;boolean&gt; 是否使用主机网络模式，默认为false，如果设置为true，表示使用宿主机网络&#x000A;- volumes &lt;[]Object&gt; 存储卷，用于定义Pod上面挂在的存储信息&#x000A;- restartPolicy &lt;string&gt; 重启策略，表示Pod在遇到故障的时候的处理策略&#x000A;&#x000A;#### 5.2 Pod配置&#x000A;&#x000A;本小节主要来研究`pod.spec.containers`属性，这也是pod配置中最为关键的一项配置。&#x000A;&#x000A;&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# kubectl explain pod.spec.containers&#x000A;KIND:     Pod&#x000A;VERSION:  v1&#x000A;RESOURCE: containers &lt;[]Object&gt;   # 数组，代表可以有多个容器&#x000A;FIELDS:&#x000A;   name  &lt;string&gt;     # 容器名称&#x000A;   image &lt;string&gt;     # 容器需要的镜像地址&#x000A;   imagePullPolicy  &lt;string&gt; # 镜像拉取策略 &#x000A;   command  &lt;[]string&gt; # 容器的启动命令列表，如不指定，使用打包时使用的启动命令&#x000A;   args     &lt;[]string&gt; # 容器的启动命令需要的参数列表&#x000A;   env      &lt;[]Object&gt; # 容器环境变量的配置&#x000A;   ports    &lt;[]Object&gt;     # 容器需要暴露的端口号列表&#x000A;   resources &lt;Object&gt;      # 资源限制和资源请求的设置&#x000A;```&#x000A;&#x000A;##### 5.2.1 基本配置&#x000A;&#x000A;创建pod-base.yaml文件，内容如下：&#x000A;&#x000A;&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-base&#x000A;  namespace: dev&#x000A;  labels:&#x000A;    user: heima&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  - name: busybox&#x000A;    image: busybox:1.30&#x000A;```&#x000A;&#x000A;![image-20210617223823675](Kubenetes.assets/image-20210617223823675-1626781695411.png)&#x000A;&#x000A;上面定义了一个比较简单Pod的配置，里面有两个容器：&#x000A;&#x000A;- nginx：用1.17.1版本的nginx镜像创建，（nginx是一个轻量级web容器）&#x000A;- busybox：用1.30版本的busybox镜像创建，（busybox是一个小巧的linux命令集合）&#x000A;&#x000A;&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 pod]# kubectl apply -f pod-base.yaml&#x000A;pod/pod-base created&#x000A;&#x000A;# 查看Pod状况&#x000A;# READY 1/2 : 表示当前Pod中有2个容器，其中1个准备就绪，1个未就绪&#x000A;# RESTARTS  : 重启次数，因为有1个容器故障了，Pod一直在重启试图恢复它&#x000A;[root@k8s-master01 pod]# kubectl get pod -n dev&#x000A;NAME       READY   STATUS    RESTARTS   AGE&#x000A;pod-base   1/2     Running   4          95s&#x000A;&#x000A;# 可以通过describe查看内部的详情&#x000A;# 此时已经运行起来了一个基本的Pod，虽然它暂时有问题&#x000A;[root@k8s-master01 pod]# kubectl describe pod pod-base -n dev&#x000A;```&#x000A;&#x000A;##### 5.2.2 镜像拉取&#x000A;&#x000A;创建pod-imagepullpolicy.yaml文件，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-imagepullpolicy&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    imagePullPolicy: Never # 用于设置镜像拉取策略&#x000A;  - name: busybox&#x000A;    image: busybox:1.30&#x000A;```&#x000A;&#x000A;![image-20210617223923659](Kubenetes.assets/image-20210617223923659.png)&#x000A;&#x000A;imagePullPolicy，用于设置镜像拉取策略，kubernetes支持配置三种拉取策略：&#x000A;&#x000A;- Always：总是从远程仓库拉取镜像（一直远程下载）&#x000A;- IfNotPresent：本地有则使用本地镜像，本地没有则从远程仓库拉取镜像（本地有就本地 本地没远程下载）&#x000A;- Never：只使用本地镜像，从不去远程仓库拉取，本地没有就报错 （一直使用本地）&#x000A;&#x000A;&gt; 默认值说明：&#x000A;&gt;&#x000A;&gt; 如果镜像tag为具体版本号， 默认策略是：IfNotPresent&#x000A;&gt;&#x000A;&gt; 如果镜像tag为：latest（最终版本） ，默认策略是always&#x000A;&#x000A;&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 pod]# kubectl create -f pod-imagepullpolicy.yaml&#x000A;pod/pod-imagepullpolicy created&#x000A;&#x000A;# 查看Pod详情&#x000A;# 此时明显可以看到nginx镜像有一步Pulling image &quot;nginx:1.17.1&quot;的过程&#x000A;[root@k8s-master01 pod]# kubectl describe pod pod-imagepullpolicy -n dev&#x000A;......&#x000A;Events:&#x000A;  Type     Reason     Age               From               Message&#x000A;  ----     ------     ----              ----               -------&#x000A;  Normal   Scheduled  &lt;unknown&gt;         default-scheduler  Successfully assigned dev/pod-imagePullPolicy to node1&#x000A;  Normal   Pulling    32s               kubelet, node1     Pulling image &quot;nginx:1.17.1&quot;&#x000A;  Normal   Pulled     26s               kubelet, node1     Successfully pulled image &quot;nginx:1.17.1&quot;&#x000A;  Normal   Created    26s               kubelet, node1     Created container nginx&#x000A;  Normal   Started    25s               kubelet, node1     Started container nginx&#x000A;  Normal   Pulled     7s (x3 over 25s)  kubelet, node1     Container image &quot;busybox:1.30&quot; already present on machine&#x000A;  Normal   Created    7s (x3 over 25s)  kubelet, node1     Created container busybox&#x000A;  Normal   Started    7s (x3 over 25s)  kubelet, node1     Started container busybox&#x000A;```&#x000A;&#x000A;##### 5.2.3 启动命令&#x000A;&#x000A;在前面的案例中，一直有一个问题没有解决，就是的busybox容器一直没有成功运行，那么到底是什么原因导致这个容器的故障呢？&#x000A;&#x000A;原来busybox并不是一个程序，而是类似于一个工具类的集合，kubernetes集群启动管理后，它会自动关闭。解决方法就是让其一直在运行，这就用到了command配置。&#x000A;&#x000A;创建pod-command.yaml文件，内容如下：&#x000A;&#x000A;&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-command&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  - name: busybox&#x000A;    image: busybox:1.30&#x000A;    command: [&quot;/bin/sh&quot;,&quot;-c&quot;,&quot;touch /tmp/hello.txt;while true;do /bin/echo $(date +%T) &gt;&gt; /tmp/hello.txt; sleep 3; done;&quot;]&#x000A;```&#x000A;&#x000A;![image-20210617224457945](Kubenetes.assets/image-20210617224457945.png)&#x000A;&#x000A;command，用于在pod中的容器初始化完毕之后运行一个命令。&#x000A;&#x000A;&gt; 稍微解释下上面命令的意思：&#x000A;&gt;&#x000A;&gt; &quot;/bin/sh&quot;,&quot;-c&quot;, 使用sh执行命令&#x000A;&gt;&#x000A;&gt; touch /tmp/hello.txt; 创建一个/tmp/hello.txt 文件&#x000A;&gt;&#x000A;&gt; while true;do /bin/echo $(date +%T) &gt;&gt; /tmp/hello.txt; sleep 3; done; 每隔3秒向文件中写入当前时间&#x000A;&#x000A;&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 pod]# kubectl create  -f pod-command.yaml&#x000A;pod/pod-command created&#x000A;&#x000A;# 查看Pod状态&#x000A;# 此时发现两个pod都正常运行了&#x000A;[root@k8s-master01 pod]# kubectl get pods pod-command -n dev&#x000A;NAME          READY   STATUS   RESTARTS   AGE&#x000A;pod-command   2/2     Runing   0          2s&#x000A;&#x000A;# 进入pod中的busybox容器，查看文件内容&#x000A;# 补充一个命令: kubectl exec  pod名称 -n 命名空间 -it -c 容器名称 /bin/sh  在容器内部执行命令&#x000A;# 使用这个命令就可以进入某个容器的内部，然后进行相关操作了&#x000A;# 比如，可以查看txt文件的内容&#x000A;[root@k8s-master01 pod]# kubectl exec pod-command -n dev -it -c busybox /bin/sh&#x000A;/ # tail -f /tmp/hello.txt&#x000A;14:44:19&#x000A;14:44:22&#x000A;14:44:25&#x000A;```&#x000A;&#x000A;```&#x000A;特别说明：&#x000A;    通过上面发现command已经可以完成启动命令和传递参数的功能，为什么这里还要提供一个args选项，用于传递参数呢?这其实跟docker有点关系，kubernetes中的command、args两项其实是实现覆盖Dockerfile中ENTRYPOINT的功能。&#x000A; 1 如果command和args均没有写，那么用Dockerfile的配置。&#x000A; 2 如果command写了，但args没有写，那么Dockerfile默认的配置会被忽略，执行输入的command&#x000A; 3 如果command没写，但args写了，那么Dockerfile中配置的ENTRYPOINT的命令会被执行，使用当前args的参数&#x000A; 4 如果command和args都写了，那么Dockerfile的配置被忽略，执行command并追加上args参数&#x000A;```&#x000A;&#x000A;##### 5.2.4 环境变量&#x000A;&#x000A;创建pod-env.yaml文件，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-env&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: busybox&#x000A;    image: busybox:1.30&#x000A;    command: [&quot;/bin/sh&quot;,&quot;-c&quot;,&quot;while true;do /bin/echo $(date +%T);sleep 60; done;&quot;]&#x000A;    env: # 设置环境变量列表&#x000A;    - name: &quot;username&quot;&#x000A;      value: &quot;admin&quot;&#x000A;    - name: &quot;password&quot;&#x000A;      value: &quot;123456&quot;&#x000A;```&#x000A;&#x000A;env，环境变量，用于在pod中的容器设置环境变量。&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-env.yaml&#x000A;pod/pod-env created&#x000A;&#x000A;# 进入容器，输出环境变量&#x000A;[root@k8s-master01 ~]# kubectl exec pod-env -n dev -c busybox -it /bin/sh&#x000A;/ # echo $username&#x000A;admin&#x000A;/ # echo $password&#x000A;123456&#x000A;```&#x000A;&#x000A;这种方式不是很推荐，推荐将这些配置单独存储在配置文件中，这种方式将在后面介绍。&#x000A;&#x000A;##### 5.2.5 端口设置&#x000A;&#x000A;本小节来介绍容器的端口设置，也就是containers的ports选项。&#x000A;&#x000A;首先看下ports支持的子选项：&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# kubectl explain pod.spec.containers.ports&#x000A;KIND:     Pod&#x000A;VERSION:  v1&#x000A;RESOURCE: ports &lt;[]Object&gt;&#x000A;FIELDS:&#x000A;   name         &lt;string&gt;  # 端口名称，如果指定，必须保证name在pod中是唯一的		&#x000A;   containerPort&lt;integer&gt; # 容器要监听的端口(0&lt;x&lt;65536)&#x000A;   hostPort     &lt;integer&gt; # 容器要在主机上公开的端口，如果设置，主机上只能运行容器的一个副本(一般省略) &#x000A;   hostIP       &lt;string&gt;  # 要将外部端口绑定到的主机IP(一般省略)&#x000A;   protocol     &lt;string&gt;  # 端口协议。必须是UDP、TCP或SCTP。默认为“TCP”。&#x000A;```&#x000A;&#x000A;接下来，编写一个测试案例，创建pod-ports.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-ports&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    ports: # 设置容器暴露的端口列表&#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;      protocol: TCP&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-ports.yaml&#x000A;pod/pod-ports created&#x000A;&#x000A;# 查看pod&#x000A;# 在下面可以明显看到配置信息&#x000A;[root@k8s-master01 ~]# kubectl get pod pod-ports -n dev -o yaml&#x000A;......&#x000A;spec:&#x000A;  containers:&#x000A;  - image: nginx:1.17.1&#x000A;    imagePullPolicy: IfNotPresent&#x000A;    name: nginx&#x000A;    ports:&#x000A;    - containerPort: 80&#x000A;      name: nginx-port&#x000A;      protocol: TCP&#x000A;......&#x000A;```&#x000A;&#x000A;访问容器中的程序需要使用的是`Podip:containerPort`&#x000A;&#x000A;##### 5.2.6 资源配额&#x000A;&#x000A;容器中的程序要运行，肯定是要占用一定资源的，比如cpu和内存等，如果不对某个容器的资源做限制，那么它就可能吃掉大量资源，导致其它容器无法运行。针对这种情况，kubernetes提供了对内存和cpu的资源进行配额的机制，这种机制主要通过resources选项实现，他有两个子选项：&#x000A;&#x000A;- limits：用于限制运行时容器的最大占用资源，当容器占用资源超过limits时会被终止，并进行重启&#x000A;- requests ：用于设置容器需要的最小资源，如果环境资源不够，容器将无法启动&#x000A;&#x000A;可以通过上面两个选项设置资源的上下限。&#x000A;&#x000A;接下来，编写一个测试案例，创建pod-resources.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-resources&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    resources: # 资源配额&#x000A;      limits:  # 限制资源（上限）&#x000A;        cpu: &quot;2&quot; # CPU限制，单位是core数&#x000A;        memory: &quot;10Gi&quot; # 内存限制&#x000A;      requests: # 请求资源（下限）&#x000A;        cpu: &quot;1&quot;  # CPU限制，单位是core数&#x000A;        memory: &quot;10Mi&quot;  # 内存限制&#x000A;```&#x000A;&#x000A;在这对cpu和memory的单位做一个说明：&#x000A;&#x000A;- cpu：core数，可以为整数或小数&#x000A;- memory： 内存大小，可以使用Gi、Mi、G、M等形式&#x000A;&#x000A;```shell&#x000A;# 运行Pod&#x000A;[root@k8s-master01 ~]# kubectl create  -f pod-resources.yaml&#x000A;pod/pod-resources created&#x000A;&#x000A;# 查看发现pod运行正常&#x000A;[root@k8s-master01 ~]# kubectl get pod pod-resources -n dev&#x000A;NAME            READY   STATUS    RESTARTS   AGE  &#x000A;pod-resources   1/1     Running   0          39s   &#x000A;&#x000A;# 接下来，停止Pod&#x000A;[root@k8s-master01 ~]# kubectl delete  -f pod-resources.yaml&#x000A;pod &quot;pod-resources&quot; deleted&#x000A;&#x000A;# 编辑pod，修改resources.requests.memory的值为10Gi&#x000A;[root@k8s-master01 ~]# vim pod-resources.yaml&#x000A;&#x000A;# 再次启动pod&#x000A;[root@k8s-master01 ~]# kubectl create  -f pod-resources.yaml&#x000A;pod/pod-resources created&#x000A;&#x000A;# 查看Pod状态，发现Pod启动失败&#x000A;[root@k8s-master01 ~]# kubectl get pod pod-resources -n dev -o wide&#x000A;NAME            READY   STATUS    RESTARTS   AGE          &#x000A;pod-resources   0/1     Pending   0          20s    &#x000A;&#x000A;# 查看pod详情会发现，如下提示&#x000A;[root@k8s-master01 ~]# kubectl describe pod pod-resources -n dev&#x000A;......&#x000A;Warning  FailedScheduling  35s   default-scheduler  0/3 nodes are available: 1 node(s) had taint {node-role.kubernetes.io/master: }, that the pod didn&#39;t tolerate, 2 Insufficient memory.(内存不足)&#x000A;```&#x000A;&#x000A;#### 5.3 Pod生命周期&#x000A;&#x000A;我们一般将pod对象从创建至终的这段时间范围称为pod的生命周期，它主要包含下面的过程：&#x000A;&#x000A;- pod创建过程&#x000A;- 运行初始化容器（init container）过程&#x000A;- 运行主容器（main container）&#x000A;  - 容器启动后钩子（post start）、容器终止前钩子（pre stop）&#x000A;  - 容器的存活性探测（liveness probe）、就绪性探测（readiness probe）&#x000A;- pod终止过程&#x000A;&#x000A;![image-20200412111402706](Kubenetes.assets/image-20200412111402706-1626782188724.png)&#x000A;&#x000A;在整个生命周期中，Pod会出现5种**状态**（**相位**），分别如下：&#x000A;&#x000A;- 挂起（Pending）：apiserver已经创建了pod资源对象，但它尚未被调度完成或者仍处于下载镜像的过程中&#x000A;- 运行中（Running）：pod已经被调度至某节点，并且所有容器都已经被kubelet创建完成&#x000A;- 成功（Succeeded）：pod中的所有容器都已经成功终止并且不会被重启&#x000A;- 失败（Failed）：所有容器都已经终止，但至少有一个容器终止失败，即容器返回了非0值的退出状态&#x000A;- 未知（Unknown）：apiserver无法正常获取到pod对象的状态信息，通常由网络通信失败所导致&#x000A;&#x000A;##### 5.3.1 创建和终止&#x000A;&#x000A;**pod的创建过程**&#x000A;&#x000A;1. 用户通过kubectl或其他api客户端提交需要创建的pod信息给apiServer&#x000A;&#x000A;2. apiServer开始生成pod对象的信息，并将信息存入etcd，然后返回确认信息至客户端&#x000A;&#x000A;3. apiServer开始反映etcd中的pod对象的变化，其它组件使用watch机制来跟踪检查apiServer上的变动&#x000A;&#x000A;4. scheduler发现有新的pod对象要创建，开始为Pod分配主机并将结果信息更新至apiServer&#x000A;&#x000A;5. node节点上的kubelet发现有pod调度过来，尝试调用docker启动容器，并将结果回送至apiServer&#x000A;&#x000A;6. apiServer将接收到的pod状态信息存入etcd中&#x000A;&#x000A;   ![image-20200406184656917](Kubenetes.assets/image-20200406184656917-1626782168787.png)&#x000A;&#x000A;**pod的终止过程**&#x000A;&#x000A;1. 用户向apiServer发送删除pod对象的命令&#x000A;2. apiServcer中的pod对象信息会随着时间的推移而更新，在宽限期内（默认30s），pod被视为dead&#x000A;3. 将pod标记为terminating状态&#x000A;4. kubelet在监控到pod对象转为terminating状态的同时启动pod关闭过程&#x000A;5. 端点控制器监控到pod对象的关闭行为时将其从所有匹配到此端点的service资源的端点列表中移除&#x000A;6. 如果当前pod对象定义了preStop钩子处理器，则在其标记为terminating后即会以同步的方式启动执行&#x000A;7. pod对象中的容器进程收到停止信号&#x000A;8. 宽限期结束后，若pod中还存在仍在运行的进程，那么pod对象会收到立即终止的信号&#x000A;9. kubelet请求apiServer将此pod资源的宽限期设置为0从而完成删除操作，此时pod对于用户已不可见&#x000A;&#x000A;##### 5.3.2 初始化容器&#x000A;&#x000A;初始化容器是在pod的主容器启动之前要运行的容器，主要是做一些主容器的前置工作，它具有两大特征：&#x000A;&#x000A;1. 初始化容器必须运行完成直至结束，若某初始化容器运行失败，那么kubernetes需要重启它直到成功完成&#x000A;2. 初始化容器必须按照定义的顺序执行，当且仅当前一个成功之后，后面的一个才能运行&#x000A;&#x000A;初始化容器有很多的应用场景，下面列出的是最常见的几个：&#x000A;&#x000A;- 提供主容器镜像中不具备的工具程序或自定义代码&#x000A;- 初始化容器要先于应用容器串行启动并运行完成，因此可用于延后应用容器的启动直至其依赖的条件得到满足&#x000A;&#x000A;接下来做一个案例，模拟下面这个需求：&#x000A;&#x000A;假设要以主容器来运行nginx，但是要求在运行nginx之前先要能够连接上mysql和redis所在服务器&#x000A;&#x000A;为了简化测试，事先规定好mysql`(192.168.90.14)`和redis`(192.168.90.15)`服务器的地址&#x000A;&#x000A;创建pod-initcontainer.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-initcontainer&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: main-container&#x000A;    image: nginx:1.17.1&#x000A;    ports: &#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;  initContainers:&#x000A;  - name: test-mysql&#x000A;    image: busybox:1.30&#x000A;    command: [&#39;sh&#39;, &#39;-c&#39;, &#39;until ping 192.168.90.14 -c 1 ; do echo waiting for mysql...; sleep 2; done;&#39;]&#x000A;  - name: test-redis&#x000A;    image: busybox:1.30&#x000A;    command: [&#39;sh&#39;, &#39;-c&#39;, &#39;until ping 192.168.90.15 -c 1 ; do echo waiting for reids...; sleep 2; done;&#39;]&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-initcontainer.yaml&#x000A;pod/pod-initcontainer created&#x000A;&#x000A;# 查看pod状态&#x000A;# 发现pod卡在启动第一个初始化容器过程中，后面的容器不会运行&#x000A;root@k8s-master01 ~]# kubectl describe pod  pod-initcontainer -n dev&#x000A;........&#x000A;Events:&#x000A;  Type    Reason     Age   From               Message&#x000A;  ----    ------     ----  ----               -------&#x000A;  Normal  Scheduled  49s   default-scheduler  Successfully assigned dev/pod-initcontainer to node1&#x000A;  Normal  Pulled     48s   kubelet, node1     Container image &quot;busybox:1.30&quot; already present on machine&#x000A;  Normal  Created    48s   kubelet, node1     Created container test-mysql&#x000A;  Normal  Started    48s   kubelet, node1     Started container test-mysql&#x000A;&#x000A;# 动态查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-initcontainer -n dev -w&#x000A;NAME                             READY   STATUS     RESTARTS   AGE&#x000A;pod-initcontainer                0/1     Init:0/2   0          15s&#x000A;pod-initcontainer                0/1     Init:1/2   0          52s&#x000A;pod-initcontainer                0/1     Init:1/2   0          53s&#x000A;pod-initcontainer                0/1     PodInitializing   0          89s&#x000A;pod-initcontainer                1/1     Running           0          90s&#x000A;&#x000A;# 接下来新开一个shell，为当前服务器新增两个ip，观察pod的变化&#x000A;[root@k8s-master01 ~]# ifconfig ens33:1 192.168.90.14 netmask 255.255.255.0 up&#x000A;[root@k8s-master01 ~]# ifconfig ens33:2 192.168.90.15 netmask 255.255.255.0 up&#x000A;```&#x000A;&#x000A;##### 5.3.3 钩子函数&#x000A;&#x000A;钩子函数能够感知自身生命周期中的事件，并在相应的时刻到来时运行用户指定的程序代码。&#x000A;&#x000A;kubernetes在主容器的启动之后和停止之前提供了两个钩子函数：&#x000A;&#x000A;- post start：容器创建之后执行，如果失败了会重启容器&#x000A;- pre stop ：容器终止之前执行，执行完成之后容器将成功终止，在其完成之前会阻塞删除容器的操作&#x000A;&#x000A;钩子处理器支持使用下面三种方式定义动作：&#x000A;&#x000A;- Exec命令：在容器内执行一次命令&#x000A;&#x000A;  ```yaml&#x000A;  ……&#x000A;    lifecycle:&#x000A;      postStart: &#x000A;        exec:&#x000A;          command:&#x000A;          - cat&#x000A;          - /tmp/healthy&#x000A;  ……&#x000A;  ```&#x000A;  &#x000A;- TCPSocket：在当前容器尝试访问指定的socket&#x000A;&#x000A;  ```yaml&#x000A;  ……      &#x000A;    lifecycle:&#x000A;      postStart:&#x000A;        tcpSocket:&#x000A;          port: 8080&#x000A;  ……&#x000A;  ```&#x000A;  &#x000A;- HTTPGet：在当前容器中向某url发起http请求&#x000A;&#x000A;  ```yaml&#x000A;  ……&#x000A;    lifecycle:&#x000A;      postStart:&#x000A;        httpGet:&#x000A;          path: / #URI地址&#x000A;          port: 80 #端口号&#x000A;          host: 192.168.5.3 #主机地址&#x000A;          scheme: HTTP #支持的协议，http或者https&#x000A;  ……&#x000A;  ```&#x000A;&#x000A;接下来，以exec方式为例，演示下钩子函数的使用，创建pod-hook-exec.yaml文件，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-hook-exec&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: main-container&#x000A;    image: nginx:1.17.1&#x000A;    ports:&#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;    lifecycle:&#x000A;      postStart: &#x000A;        exec: # 在容器启动的时候执行一个命令，修改掉nginx的默认首页内容&#x000A;          command: [&quot;/bin/sh&quot;, &quot;-c&quot;, &quot;echo postStart... &gt; /usr/share/nginx/html/index.html&quot;]&#x000A;      preStop:&#x000A;        exec: # 在容器停止之前停止nginx服务&#x000A;          command: [&quot;/usr/sbin/nginx&quot;,&quot;-s&quot;,&quot;quit&quot;]&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-hook-exec.yaml&#x000A;pod/pod-hook-exec created&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pods  pod-hook-exec -n dev -o wide&#x000A;NAME           READY   STATUS     RESTARTS   AGE    IP            NODE    &#x000A;pod-hook-exec  1/1     Running    0          29s    10.244.2.48   node2   &#x000A;&#x000A;# 访问pod&#x000A;[root@k8s-master01 ~]# curl 10.244.2.48&#x000A;postStart...&#x000A;```&#x000A;&#x000A;##### 5.3.4 容器探测&#x000A;&#x000A;容器探测用于检测容器中的应用实例是否正常工作，是保障业务可用性的一种传统机制。如果经过探测，实例的状态不符合预期，那么kubernetes就会把该问题实例&quot; 摘除 &quot;，不承担业务流量。kubernetes提供了两种探针来实现容器探测，分别是：&#x000A;&#x000A;- liveness probes：存活性探针，用于检测应用实例当前是否处于正常运行状态，如果不是，k8s会重启容器&#x000A;- readiness probes：就绪性探针，用于检测应用实例当前是否可以接收请求，如果不能，k8s不会转发流量&#x000A;&#x000A;&gt; livenessProbe 决定是否重启容器，readinessProbe 决定是否将请求转发给容器。&#x000A;&#x000A;上面两种探针目前均支持三种探测方式：&#x000A;&#x000A;- Exec命令：在容器内执行一次命令，如果命令执行的退出码为0，则认为程序正常，否则不正常&#x000A;&#x000A;  ```yaml&#x000A;  ……&#x000A;    livenessProbe:&#x000A;      exec:&#x000A;        command:&#x000A;        - cat&#x000A;        - /tmp/healthy&#x000A;  ……&#x000A;  ```&#x000A;  &#x000A;- TCPSocket：将会尝试访问一个用户容器的端口，如果能够建立这条连接，则认为程序正常，否则不正常&#x000A;&#x000A;  ```yaml&#x000A;  ……      &#x000A;    livenessProbe:&#x000A;      tcpSocket:&#x000A;        port: 8080&#x000A;  ……&#x000A;  ```&#x000A;  &#x000A;- HTTPGet：调用容器内Web应用的URL，如果返回的状态码在200和399之间，则认为程序正常，否则不正常&#x000A;&#x000A;  ```yaml&#x000A;  ……&#x000A;    livenessProbe:&#x000A;      httpGet:&#x000A;        path: / #URI地址&#x000A;        port: 80 #端口号&#x000A;        host: 127.0.0.1 #主机地址&#x000A;        scheme: HTTP #支持的协议，http或者https&#x000A;  ……&#x000A;  ```&#x000A;&#x000A;下面以liveness probes为例，做几个演示：&#x000A;&#x000A;**方式一：Exec**&#x000A;&#x000A;创建pod-liveness-exec.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-liveness-exec&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    ports: &#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;    livenessProbe:&#x000A;      exec:&#x000A;        command: [&quot;/bin/cat&quot;,&quot;/tmp/hello.txt&quot;] # 执行一个查看文件的命令&#x000A;```&#x000A;&#x000A;创建pod，观察效果&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-liveness-exec.yaml&#x000A;pod/pod-liveness-exec created&#x000A;&#x000A;# 查看Pod详情&#x000A;[root@k8s-master01 ~]# kubectl describe pods pod-liveness-exec -n dev&#x000A;......&#x000A;  Normal   Created    20s (x2 over 50s)  kubelet, node1     Created container nginx&#x000A;  Normal   Started    20s (x2 over 50s)  kubelet, node1     Started container nginx&#x000A;  Normal   Killing    20s                kubelet, node1     Container nginx failed liveness probe, will be restarted&#x000A;  Warning  Unhealthy  0s (x5 over 40s)   kubelet, node1     Liveness probe failed: cat: can&#39;t open &#39;/tmp/hello11.txt&#39;: No such file or directory&#x000A;  &#x000A;# 观察上面的信息就会发现nginx容器启动之后就进行了健康检查&#x000A;# 检查失败之后，容器被kill掉，然后尝试进行重启（这是重启策略的作用，后面讲解）&#x000A;# 稍等一会之后，再观察pod信息，就可以看到RESTARTS不再是0，而是一直增长&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-liveness-exec -n dev&#x000A;NAME                READY   STATUS             RESTARTS   AGE&#x000A;pod-liveness-exec   0/1     CrashLoopBackOff   2          3m19s&#x000A;&#x000A;# 当然接下来，可以修改成一个存在的文件，比如/tmp/hello.txt，再试，结果就正常了......&#x000A;```&#x000A;&#x000A;**方式二：TCPSocket**&#x000A;&#x000A;创建pod-liveness-tcpsocket.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-liveness-tcpsocket&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    ports: &#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;    livenessProbe:&#x000A;      tcpSocket:&#x000A;        port: 8080 # 尝试访问8080端口&#x000A;```&#x000A;&#x000A;创建pod，观察效果&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-liveness-tcpsocket.yaml&#x000A;pod/pod-liveness-tcpsocket created&#x000A;&#x000A;# 查看Pod详情&#x000A;[root@k8s-master01 ~]# kubectl describe pods pod-liveness-tcpsocket -n dev&#x000A;......&#x000A;  Normal   Scheduled  31s                            default-scheduler  Successfully assigned dev/pod-liveness-tcpsocket to node2&#x000A;  Normal   Pulled     &lt;invalid&gt;                      kubelet, node2     Container image &quot;nginx:1.17.1&quot; already present on machine&#x000A;  Normal   Created    &lt;invalid&gt;                      kubelet, node2     Created container nginx&#x000A;  Normal   Started    &lt;invalid&gt;                      kubelet, node2     Started container nginx&#x000A;  Warning  Unhealthy  &lt;invalid&gt; (x2 over &lt;invalid&gt;)  kubelet, node2     Liveness probe failed: dial tcp 10.244.2.44:8080: connect: connection refused&#x000A;  &#x000A;# 观察上面的信息，发现尝试访问8080端口,但是失败了&#x000A;# 稍等一会之后，再观察pod信息，就可以看到RESTARTS不再是0，而是一直增长&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-liveness-tcpsocket  -n dev&#x000A;NAME                     READY   STATUS             RESTARTS   AGE&#x000A;pod-liveness-tcpsocket   0/1     CrashLoopBackOff   2          3m19s&#x000A;&#x000A;# 当然接下来，可以修改成一个可以访问的端口，比如80，再试，结果就正常了......&#x000A;```&#x000A;&#x000A;**方式三：HTTPGet**&#x000A;&#x000A;创建pod-liveness-httpget.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-liveness-httpget&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    ports:&#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;    livenessProbe:&#x000A;      httpGet:  # 其实就是访问http://127.0.0.1:80/hello  &#x000A;        scheme: HTTP #支持的协议，http或者https&#x000A;        port: 80 #端口号&#x000A;        path: /hello #URI地址&#x000A;```&#x000A;&#x000A;创建pod，观察效果&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-liveness-httpget.yaml&#x000A;pod/pod-liveness-httpget created&#x000A;&#x000A;# 查看Pod详情&#x000A;[root@k8s-master01 ~]# kubectl describe pod pod-liveness-httpget -n dev&#x000A;.......&#x000A;  Normal   Pulled     6s (x3 over 64s)  kubelet, node1     Container image &quot;nginx:1.17.1&quot; already present on machine&#x000A;  Normal   Created    6s (x3 over 64s)  kubelet, node1     Created container nginx&#x000A;  Normal   Started    6s (x3 over 63s)  kubelet, node1     Started container nginx&#x000A;  Warning  Unhealthy  6s (x6 over 56s)  kubelet, node1     Liveness probe failed: HTTP probe failed with statuscode: 404&#x000A;  Normal   Killing    6s (x2 over 36s)  kubelet, node1     Container nginx failed liveness probe, will be restarted&#x000A;  &#x000A;# 观察上面信息，尝试访问路径，但是未找到,出现404错误&#x000A;# 稍等一会之后，再观察pod信息，就可以看到RESTARTS不再是0，而是一直增长&#x000A;[root@k8s-master01 ~]# kubectl get pod pod-liveness-httpget -n dev&#x000A;NAME                   READY   STATUS    RESTARTS   AGE&#x000A;pod-liveness-httpget   1/1     Running   5          3m17s&#x000A;&#x000A;# 当然接下来，可以修改成一个可以访问的路径path，比如/，再试，结果就正常了......&#x000A;```&#x000A;&#x000A;至此，已经使用liveness Probe演示了三种探测方式，但是查看livenessProbe的子属性，会发现除了这三种方式，还有一些其他的配置，在这里一并解释下：&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# kubectl explain pod.spec.containers.livenessProbe&#x000A;FIELDS:&#x000A;   exec &lt;Object&gt;  &#x000A;   tcpSocket    &lt;Object&gt;&#x000A;   httpGet      &lt;Object&gt;&#x000A;   initialDelaySeconds  &lt;integer&gt;  # 容器启动后等待多少秒执行第一次探测&#x000A;   timeoutSeconds       &lt;integer&gt;  # 探测超时时间。默认1秒，最小1秒&#x000A;   periodSeconds        &lt;integer&gt;  # 执行探测的频率。默认是10秒，最小1秒&#x000A;   failureThreshold     &lt;integer&gt;  # 连续探测失败多少次才被认定为失败。默认是3。最小值是1&#x000A;   successThreshold     &lt;integer&gt;  # 连续探测成功多少次才被认定为成功。默认是1&#x000A;```&#x000A;&#x000A;下面稍微配置两个，演示下效果即可：&#x000A;&#x000A;```yaml&#x000A;[root@k8s-master01 ~]# more pod-liveness-httpget.yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-liveness-httpget&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    ports:&#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;    livenessProbe:&#x000A;      httpGet:&#x000A;        scheme: HTTP&#x000A;        port: 80 &#x000A;        path: /&#x000A;      initialDelaySeconds: 30 # 容器启动后30s开始探测&#x000A;      timeoutSeconds: 5 # 探测超时时间为5s&#x000A;```&#x000A;&#x000A;##### 5.3.5 重启策略&#x000A;&#x000A;在上一节中，一旦容器探测出现了问题，kubernetes就会对容器所在的Pod进行重启，其实这是由pod的重启策略决定的，pod的重启策略有 3 种，分别如下：&#x000A;&#x000A;- Always ：容器失效时，自动重启该容器，这也是默认值。&#x000A;- OnFailure ： 容器终止运行且退出码不为0时重启&#x000A;- Never ： 不论状态为何，都不重启该容器&#x000A;&#x000A;重启策略适用于pod对象中的所有容器，首次需要重启的容器，将在其需要时立即进行重启，随后再次需要重启的操作将由kubelet延迟一段时间后进行，且反复的重启操作的延迟时长以此为10s、20s、40s、80s、160s和300s，300s是最大延迟时长。&#x000A;&#x000A;创建pod-restartpolicy.yaml：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-restartpolicy&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    ports:&#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;    livenessProbe:&#x000A;      httpGet:&#x000A;        scheme: HTTP&#x000A;        port: 80&#x000A;        path: /hello&#x000A;  restartPolicy: Never # 设置重启策略为Never&#x000A;```&#x000A;&#x000A;运行Pod测试&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-restartpolicy.yaml&#x000A;pod/pod-restartpolicy created&#x000A;&#x000A;# 查看Pod详情，发现nginx容器失败&#x000A;[root@k8s-master01 ~]# kubectl  describe pods pod-restartpolicy  -n dev&#x000A;......&#x000A;  Warning  Unhealthy  15s (x3 over 35s)  kubelet, node1     Liveness probe failed: HTTP probe failed with statuscode: 404&#x000A;  Normal   Killing    15s                kubelet, node1     Container nginx failed liveness probe&#x000A;  &#x000A;# 多等一会，再观察pod的重启次数，发现一直是0，并未重启   &#x000A;[root@k8s-master01 ~]# kubectl  get pods pod-restartpolicy -n dev&#x000A;NAME                   READY   STATUS    RESTARTS   AGE&#x000A;pod-restartpolicy      0/1     Running   0          5min42s&#x000A;```&#x000A;&#x000A;#### 5.4 Pod调度&#x000A;&#x000A;在默认情况下，一个Pod在哪个Node节点上运行，是由Scheduler组件采用相应的算法计算出来的，这个过程是不受人工控制的。但是在实际使用中，这并不满足的需求，因为很多情况下，我们想控制某些Pod到达某些节点上，那么应该怎么做呢？这就要求了解kubernetes对Pod的调度规则，kubernetes提供了四大类调度方式：&#x000A;&#x000A;- 自动调度：运行在哪个节点上完全由Scheduler经过一系列的算法计算得出&#x000A;- 定向调度：NodeName、NodeSelector&#x000A;- 亲和性调度：NodeAffinity、PodAffinity、PodAntiAffinity&#x000A;- 污点（容忍）调度：Taints、Toleration&#x000A;&#x000A;##### 5.4.1 定向调度&#x000A;&#x000A;定向调度，指的是利用在pod上声明nodeName或者nodeSelector，以此将Pod调度到期望的node节点上。注意，这里的调度是强制的，这就意味着即使要调度的目标Node不存在，也会向上面进行调度，只不过pod运行失败而已。&#x000A;&#x000A;**NodeName**&#x000A;&#x000A;NodeName用于强制约束将Pod调度到指定的Name的Node节点上。这种方式，其实是直接跳过Scheduler的调度逻辑，直接将Pod调度到指定名称的节点。&#x000A;&#x000A;接下来，实验一下：创建一个pod-nodename.yaml文件&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-nodename&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  nodeName: node1 # 指定调度到node1节点上&#x000A;```&#x000A;&#x000A;```shell&#x000A;#创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-nodename.yaml&#x000A;pod/pod-nodename created&#x000A;&#x000A;#查看Pod调度到NODE属性，确实是调度到了node1节点上&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-nodename -n dev -o wide&#x000A;NAME           READY   STATUS    RESTARTS   AGE   IP            NODE      ......&#x000A;pod-nodename   1/1     Running   0          56s   10.244.1.87   node1     ......   &#x000A;&#x000A;# 接下来，删除pod，修改nodeName的值为node3（并没有node3节点）&#x000A;[root@k8s-master01 ~]# kubectl delete -f pod-nodename.yaml&#x000A;pod &quot;pod-nodename&quot; deleted&#x000A;[root@k8s-master01 ~]# vim pod-nodename.yaml&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-nodename.yaml&#x000A;pod/pod-nodename created&#x000A;&#x000A;#再次查看，发现已经向Node3节点调度，但是由于不存在node3节点，所以pod无法正常运行&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-nodename -n dev -o wide&#x000A;NAME           READY   STATUS    RESTARTS   AGE   IP       NODE    ......&#x000A;pod-nodename   0/1     Pending   0          6s    &lt;none&gt;   node3   ......           &#x000A;```&#x000A;&#x000A;**NodeSelector**&#x000A;&#x000A;NodeSelector用于将pod调度到添加了指定标签的node节点上。它是通过kubernetes的label-selector机制实现的，也就是说，在pod创建之前，会由scheduler使用MatchNodeSelector调度策略进行label匹配，找出目标node，然后将pod调度到目标节点，该匹配规则是强制约束。&#x000A;&#x000A;接下来，实验一下：&#x000A;&#x000A;1 首先分别为node节点添加标签&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# kubectl label nodes node1 nodeenv=pro&#x000A;node/node2 labeled&#x000A;[root@k8s-master01 ~]# kubectl label nodes node2 nodeenv=test&#x000A;node/node2 labeled&#x000A;```&#x000A;&#x000A;2 创建一个pod-nodeselector.yaml文件，并使用它创建Pod&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-nodeselector&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  nodeSelector: &#x000A;    nodeenv: pro # 指定调度到具有nodeenv=pro标签的节点上&#x000A;```&#x000A;&#x000A;```shell&#x000A;#创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-nodeselector.yaml&#x000A;pod/pod-nodeselector created&#x000A;&#x000A;#查看Pod调度到NODE属性，确实是调度到了node1节点上&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-nodeselector -n dev -o wide&#x000A;NAME               READY   STATUS    RESTARTS   AGE     IP          NODE    ......&#x000A;pod-nodeselector   1/1     Running   0          47s   10.244.1.87   node1   ......&#x000A;&#x000A;# 接下来，删除pod，修改nodeSelector的值为nodeenv: xxxx（不存在打有此标签的节点）&#x000A;[root@k8s-master01 ~]# kubectl delete -f pod-nodeselector.yaml&#x000A;pod &quot;pod-nodeselector&quot; deleted&#x000A;[root@k8s-master01 ~]# vim pod-nodeselector.yaml&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-nodeselector.yaml&#x000A;pod/pod-nodeselector created&#x000A;&#x000A;#再次查看，发现pod无法正常运行,Node的值为none&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -o wide&#x000A;NAME               READY   STATUS    RESTARTS   AGE     IP       NODE    &#x000A;pod-nodeselector   0/1     Pending   0          2m20s   &lt;none&gt;   &lt;none&gt;&#x000A;&#x000A;# 查看详情,发现node selector匹配失败的提示&#x000A;[root@k8s-master01 ~]# kubectl describe pods pod-nodeselector -n dev&#x000A;.......&#x000A;Events:&#x000A;  Type     Reason            Age        From               Message&#x000A;  ----     ------            ----       ----               -------&#x000A;  Warning  FailedScheduling  &lt;unknown&gt;  default-scheduler  0/3 nodes are available: 3 node(s) didn&#39;t match node selector.&#x000A;```&#x000A;&#x000A;##### 5.4.2 亲和性调度&#x000A;&#x000A;上一节，介绍了两种定向调度的方式，使用起来非常方便，但是也有一定的问题，那就是如果没有满足条件的Node，那么Pod将不会被运行，即使在集群中还有可用Node列表也不行，这就限制了它的使用场景。&#x000A;&#x000A;基于上面的问题，kubernetes还提供了一种亲和性调度（Affinity）。它在NodeSelector的基础之上的进行了扩展，可以通过配置的形式，实现优先选择满足条件的Node进行调度，如果没有，也可以调度到不满足条件的节点上，使调度更加灵活。&#x000A;&#x000A;Affinity主要分为三类：&#x000A;&#x000A;- nodeAffinity(node亲和性）: 以node为目标，解决pod可以调度到哪些node的问题&#x000A;- podAffinity(pod亲和性) : 以pod为目标，解决pod可以和哪些已存在的pod部署在同一个拓扑域中的问题&#x000A;- podAntiAffinity(pod反亲和性) : 以pod为目标，解决pod不能和哪些已存在pod部署在同一个拓扑域中的问题&#x000A;&#x000A;&gt; 关于亲和性(反亲和性)使用场景的说明：&#x000A;&gt;&#x000A;&gt; **亲和性**：如果两个应用频繁交互，那就有必要利用亲和性让两个应用的尽可能的靠近，这样可以减少因网络通信而带来的性能损耗。&#x000A;&gt;&#x000A;&gt; **反亲和性**：当应用的采用多副本部署时，有必要采用反亲和性让各个应用实例打散分布在各个node上，这样可以提高服务的高可用性。&#x000A;&#x000A;**NodeAffinity**&#x000A;&#x000A;首先来看一下`NodeAffinity`的可配置项：&#x000A;&#x000A;```markdown&#x000A;pod.spec.affinity.nodeAffinity&#x000A;  requiredDuringSchedulingIgnoredDuringExecution  Node节点必须满足指定的所有规则才可以，相当于硬限制&#x000A;    nodeSelectorTerms  节点选择列表&#x000A;      matchFields   按节点字段列出的节点选择器要求列表&#x000A;      matchExpressions   按节点标签列出的节点选择器要求列表(推荐)&#x000A;        key    键&#x000A;        values 值&#x000A;        operat or 关系符 支持Exists, DoesNotExist, In, NotIn, Gt, Lt&#x000A;  preferredDuringSchedulingIgnoredDuringExecution 优先调度到满足指定的规则的Node，相当于软限制 (倾向)&#x000A;    preference   一个节点选择器项，与相应的权重相关联&#x000A;      matchFields   按节点字段列出的节点选择器要求列表&#x000A;      matchExpressions   按节点标签列出的节点选择器要求列表(推荐)&#x000A;        key    键&#x000A;        values 值&#x000A;        operator 关系符 支持In, NotIn, Exists, DoesNotExist, Gt, Lt&#x000A;	weight 倾向权重，在范围1-100。&#x000A;```&#x000A;&#x000A;```shell&#x000A;关系符的使用说明:&#x000A;&#x000A;- matchExpressions:&#x000A;  - key: nodeenv              # 匹配存在标签的key为nodeenv的节点&#x000A;    operator: Exists&#x000A;  - key: nodeenv              # 匹配标签的key为nodeenv,且value是&quot;xxx&quot;或&quot;yyy&quot;的节点&#x000A;    operator: In&#x000A;    values: [&quot;xxx&quot;,&quot;yyy&quot;]&#x000A;  - key: nodeenv              # 匹配标签的key为nodeenv,且value大于&quot;xxx&quot;的节点&#x000A;    operator: Gt&#x000A;    values: &quot;xxx&quot;&#x000A;```&#x000A;&#x000A;接下来首先演示一下`requiredDuringSchedulingIgnoredDuringExecution` ,&#x000A;&#x000A;创建pod-nodeaffinity-required.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-nodeaffinity-required&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  affinity:  #亲和性设置&#x000A;    nodeAffinity: #设置node亲和性&#x000A;      requiredDuringSchedulingIgnoredDuringExecution: # 硬限制&#x000A;        nodeSelectorTerms:&#x000A;        - matchExpressions: # 匹配env的值在[&quot;xxx&quot;,&quot;yyy&quot;]中的标签&#x000A;          - key: nodeenv&#x000A;            operator: In&#x000A;            values: [&quot;xxx&quot;,&quot;yyy&quot;]&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-nodeaffinity-required.yaml&#x000A;pod/pod-nodeaffinity-required created&#x000A;&#x000A;# 查看pod状态 （运行失败）&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-nodeaffinity-required -n dev -o wide&#x000A;NAME                        READY   STATUS    RESTARTS   AGE   IP       NODE    ...... &#x000A;pod-nodeaffinity-required   0/1     Pending   0          16s   &lt;none&gt;   &lt;none&gt;  ......&#x000A;&#x000A;# 查看Pod的详情&#x000A;# 发现调度失败，提示node选择失败&#x000A;[root@k8s-master01 ~]# kubectl describe pod pod-nodeaffinity-required -n dev&#x000A;......&#x000A;  Warning  FailedScheduling  &lt;unknown&gt;  default-scheduler  0/3 nodes are available: 3 node(s) didn&#39;t match node selector.&#x000A;  Warning  FailedScheduling  &lt;unknown&gt;  default-scheduler  0/3 nodes are available: 3 node(s) didn&#39;t match node selector.&#x000A;&#x000A;#接下来，停止pod&#x000A;[root@k8s-master01 ~]# kubectl delete -f pod-nodeaffinity-required.yaml&#x000A;pod &quot;pod-nodeaffinity-required&quot; deleted&#x000A;&#x000A;# 修改文件，将values: [&quot;xxx&quot;,&quot;yyy&quot;]------&gt; [&quot;pro&quot;,&quot;yyy&quot;]&#x000A;[root@k8s-master01 ~]# vim pod-nodeaffinity-required.yaml&#x000A;&#x000A;# 再次启动&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-nodeaffinity-required.yaml&#x000A;pod/pod-nodeaffinity-required created&#x000A;&#x000A;# 此时查看，发现调度成功，已经将pod调度到了node1上&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-nodeaffinity-required -n dev -o wide&#x000A;NAME                        READY   STATUS    RESTARTS   AGE   IP            NODE  ...... &#x000A;pod-nodeaffinity-required   1/1     Running   0          11s   10.244.1.89   node1 ......&#x000A;```&#x000A;&#x000A;接下来再演示一下`requiredDuringSchedulingIgnoredDuringExecution` ,&#x000A;&#x000A;创建pod-nodeaffinity-preferred.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-nodeaffinity-preferred&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  affinity:  #亲和性设置&#x000A;    nodeAffinity: #设置node亲和性&#x000A;      preferredDuringSchedulingIgnoredDuringExecution: # 软限制&#x000A;      - weight: 1&#x000A;        preference:&#x000A;          matchExpressions: # 匹配env的值在[&quot;xxx&quot;,&quot;yyy&quot;]中的标签(当前环境没有)&#x000A;          - key: nodeenv&#x000A;            operator: In&#x000A;            values: [&quot;xxx&quot;,&quot;yyy&quot;]&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-nodeaffinity-preferred.yaml&#x000A;pod/pod-nodeaffinity-preferred created&#x000A;&#x000A;# 查看pod状态 （运行成功）&#x000A;[root@k8s-master01 ~]# kubectl get pod pod-nodeaffinity-preferred -n dev&#x000A;NAME                         READY   STATUS    RESTARTS   AGE&#x000A;pod-nodeaffinity-preferred   1/1     Running   0          40s&#x000A;```&#x000A;&#x000A;```&#x000A;NodeAffinity规则设置的注意事项：&#x000A;    1 如果同时定义了nodeSelector和nodeAffinity，那么必须两个条件都得到满足，Pod才能运行在指定的Node上&#x000A;    2 如果nodeAffinity指定了多个nodeSelectorTerms，那么只需要其中一个能够匹配成功即可&#x000A;    3 如果一个nodeSelectorTerms中有多个matchExpressions ，则一个节点必须满足所有的才能匹配成功&#x000A;    4 如果一个pod所在的Node在Pod运行期间其标签发生了改变，不再符合该Pod的节点亲和性需求，则系统将忽略此变化&#x000A;```&#x000A;&#x000A;**PodAffinity**&#x000A;&#x000A;PodAffinity主要实现以运行的Pod为参照，实现让新创建的Pod跟参照pod在一个区域的功能。&#x000A;&#x000A;首先来看一下`PodAffinity`的可配置项：&#x000A;&#x000A;```markdown&#x000A;pod.spec.affinity.podAffinity&#x000A;  requiredDuringSchedulingIgnoredDuringExecution  硬限制&#x000A;    namespaces       指定参照pod的namespace&#x000A;    topologyKey      指定调度作用域&#x000A;    labelSelector    标签选择器&#x000A;      matchExpressions  按节点标签列出的节点选择器要求列表(推荐)&#x000A;        key    键&#x000A;        values 值&#x000A;        operator 关系符 支持In, NotIn, Exists, DoesNotExist.&#x000A;      matchLabels    指多个matchExpressions映射的内容&#x000A;  preferredDuringSchedulingIgnoredDuringExecution 软限制&#x000A;    podAffinityTerm  选项&#x000A;      namespaces      &#x000A;      topologyKey&#x000A;      labelSelector&#x000A;        matchExpressions  &#x000A;          key    键&#x000A;          values 值&#x000A;          operator&#x000A;        matchLabels &#x000A;    weight 倾向权重，在范围1-100&#x000A;```&#x000A;&#x000A;```markdown&#x000A;topologyKey用于指定调度时作用域,例如:&#x000A;    如果指定为kubernetes.io/hostname，那就是以Node节点为区分范围&#x000A;	如果指定为beta.kubernetes.io/os,则以Node节点的操作系统类型来区分&#x000A;```&#x000A;&#x000A;接下来，演示下`requiredDuringSchedulingIgnoredDuringExecution`,&#x000A;&#x000A;1）首先创建一个参照Pod，pod-podaffinity-target.yaml：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-podaffinity-target&#x000A;  namespace: dev&#x000A;  labels:&#x000A;    podenv: pro #设置标签&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  nodeName: node1 # 将目标pod名确指定到node1上&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 启动目标pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-podaffinity-target.yaml&#x000A;pod/pod-podaffinity-target created&#x000A;&#x000A;# 查看pod状况&#x000A;[root@k8s-master01 ~]# kubectl get pods  pod-podaffinity-target -n dev&#x000A;NAME                     READY   STATUS    RESTARTS   AGE&#x000A;pod-podaffinity-target   1/1     Running   0          4s&#x000A;```&#x000A;&#x000A;2）创建pod-podaffinity-required.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-podaffinity-required&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  affinity:  #亲和性设置&#x000A;    podAffinity: #设置pod亲和性&#x000A;      requiredDuringSchedulingIgnoredDuringExecution: # 硬限制&#x000A;      - labelSelector:&#x000A;          matchExpressions: # 匹配env的值在[&quot;xxx&quot;,&quot;yyy&quot;]中的标签&#x000A;          - key: podenv&#x000A;            operator: In&#x000A;            values: [&quot;xxx&quot;,&quot;yyy&quot;]&#x000A;        topologyKey: kubernetes.io/hostname&#x000A;```&#x000A;&#x000A;上面配置表达的意思是：新Pod必须要与拥有标签nodeenv=xxx或者nodeenv=yyy的pod在同一Node上，显然现在没有这样pod，接下来，运行测试一下。&#x000A;&#x000A;```shell&#x000A;# 启动pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-podaffinity-required.yaml&#x000A;pod/pod-podaffinity-required created&#x000A;&#x000A;# 查看pod状态，发现未运行&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-podaffinity-required -n dev&#x000A;NAME                       READY   STATUS    RESTARTS   AGE&#x000A;pod-podaffinity-required   0/1     Pending   0          9s&#x000A;&#x000A;# 查看详细信息&#x000A;[root@k8s-master01 ~]# kubectl describe pods pod-podaffinity-required  -n dev&#x000A;......&#x000A;Events:&#x000A;  Type     Reason            Age        From               Message&#x000A;  ----     ------            ----       ----               -------&#x000A;  Warning  FailedScheduling  &lt;unknown&gt;  default-scheduler  0/3 nodes are available: 2 node(s) didn&#39;t match pod affinity rules, 1 node(s) had taints that the pod didn&#39;t tolerate.&#x000A;&#x000A;# 接下来修改  values: [&quot;xxx&quot;,&quot;yyy&quot;]-----&gt;values:[&quot;pro&quot;,&quot;yyy&quot;]&#x000A;# 意思是：新Pod必须要与拥有标签nodeenv=xxx或者nodeenv=yyy的pod在同一Node上&#x000A;[root@k8s-master01 ~]# vim pod-podaffinity-required.yaml&#x000A;&#x000A;# 然后重新创建pod，查看效果&#x000A;[root@k8s-master01 ~]# kubectl delete -f  pod-podaffinity-required.yaml&#x000A;pod &quot;pod-podaffinity-required&quot; de leted&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-podaffinity-required.yaml&#x000A;pod/pod-podaffinity-required created&#x000A;&#x000A;# 发现此时Pod运行正常&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-podaffinity-required -n dev&#x000A;NAME                       READY   STATUS    RESTARTS   AGE   LABELS&#x000A;pod-podaffinity-required   1/1     Running   0          6s    &lt;none&gt;&#x000A;```&#x000A;&#x000A;关于`PodAffinity`的 `preferredDuringSchedulingIgnoredDuringExecution`，这里不再演示。&#x000A;&#x000A;**PodAntiAffinity**&#x000A;&#x000A;PodAntiAffinity主要实现以运行的Pod为参照，让新创建的Pod跟参照pod不在一个区域中的功能。&#x000A;&#x000A;它的配置方式和选项跟PodAffinty是一样的，这里不再做详细解释，直接做一个测试案例。&#x000A;&#x000A;1）继续使用上个案例中目标pod&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -o wide --show-labels&#x000A;NAME                     READY   STATUS    RESTARTS   AGE     IP            NODE    LABELS&#x000A;pod-podaffinity-required 1/1     Running   0          3m29s   10.244.1.38   node1   &lt;none&gt;     &#x000A;pod-podaffinity-target   1/1     Running   0          9m25s   10.244.1.37   node1   podenv=pro&#x000A;```&#x000A;&#x000A;2）创建pod-podantiaffinity-required.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-podantiaffinity-required&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  affinity:  #亲和性设置&#x000A;    podAntiAffinity: #设置pod亲和性&#x000A;      requiredDuringSchedulingIgnoredDuringExecution: # 硬限制&#x000A;      - labelSelector:&#x000A;          matchExpressions: # 匹配podenv的值在[&quot;pro&quot;]中的标签&#x000A;          - key: podenv&#x000A;            operator: In&#x000A;            values: [&quot;pro&quot;]&#x000A;        topologyKey: kubernetes.io/hostname&#x000A;```&#x000A;&#x000A;上面配置表达的意思是：新Pod必须要与拥有标签nodeenv=pro的pod不在同一Node上，运行测试一下。&#x000A;&#x000A;```shell&#x000A;# 创建pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-podantiaffinity-required.yaml&#x000A;pod/pod-podantiaffinity-required created&#x000A;&#x000A;# 查看pod&#x000A;# 发现调度到了node2上&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-podantiaffinity-required -n dev -o wide&#x000A;NAME                           READY   STATUS    RESTARTS   AGE   IP            NODE   .. &#x000A;pod-podantiaffinity-required   1/1     Running   0          30s   10.244.1.96   node2  ..&#x000A;```&#x000A;&#x000A;##### 5.4.3 污点和容忍&#x000A;&#x000A;**污点（Taints）**&#x000A;&#x000A;前面的调度方式都是站在Pod的角度上，通过在Pod上添加属性，来确定Pod是否要调度到指定的Node上，其实我们也可以站在Node的角度上，通过在Node上添加**污点**属性，来决定是否允许Pod调度过来。&#x000A;&#x000A;Node被设置上污点之后就和Pod之间存在了一种相斥的关系，进而拒绝Pod调度进来，甚至可以将已经存在的Pod驱逐出去。&#x000A;&#x000A;污点的格式为：`key=value:effect`, key和value是污点的标签，effect描述污点的作用，支持如下三个选项：&#x000A;&#x000A;- PreferNoSchedule：kubernetes将尽量避免把Pod调度到具有该污点的Node上，除非没有其他节点可调度&#x000A;- NoSchedule：kubernetes将不会把Pod调度到具有该污点的Node上，但不会影响当前Node上已存在的Pod&#x000A;- NoExecute：kubernetes将不会把Pod调度到具有该污点的Node上，同时也会将Node上已存在的Pod驱离&#x000A;&#x000A;![image-20200605021606508](Kubenetes.assets/image-20200605021831545.png)&#x000A;&#x000A;使用kubectl设置和去除污点的命令示例如下：&#x000A;&#x000A;```shell&#x000A;# 设置污点&#x000A;kubectl taint nodes node1 key=value:effect&#x000A;&#x000A;# 去除污点&#x000A;kubectl taint nodes node1 key:effect-&#x000A;&#x000A;# 去除所有污点&#x000A;kubectl taint nodes node1 key-&#x000A;```&#x000A;&#x000A;接下来，演示下污点的效果：&#x000A;&#x000A;1. 准备节点node1（为了演示效果更加明显，暂时停止node2节点）&#x000A;2. 为node1节点设置一个污点: `tag=heima:PreferNoSchedule`；然后创建pod1( pod1 可以 )&#x000A;3. 修改为node1节点设置一个污点: `tag=heima:NoSchedule`；然后创建pod2( pod1 正常 pod2 失败 )&#x000A;4. 修改为node1节点设置一个污点: `tag=heima:NoExecute`；然后创建pod3 ( 3个pod都失败 )&#x000A;&#x000A;```shell&#x000A;# 为node1设置污点(PreferNoSchedule)&#x000A;[root@k8s-master01 ~]# kubectl taint nodes node1 tag=heima:PreferNoSchedule&#x000A;&#x000A;# 创建pod1&#x000A;[root@k8s-master01 ~]# kubectl run taint1 --image=nginx:1.17.1 -n dev&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -o wide&#x000A;NAME                      READY   STATUS    RESTARTS   AGE     IP           NODE   &#x000A;taint1-7665f7fd85-574h4   1/1     Running   0          2m24s   10.244.1.59   node1    &#x000A;&#x000A;# 为node1设置污点(取消PreferNoSchedule，设置NoSchedule)&#x000A;[root@k8s-master01 ~]# kubectl taint nodes node1 tag:PreferNoSchedule-&#x000A;[root@k8s-master01 ~]# kubectl taint nodes node1 tag=heima:NoSchedule&#x000A;&#x000A;# 创建pod2&#x000A;[root@k8s-master01 ~]# kubectl run taint2 --image=nginx:1.17.1 -n dev&#x000A;[root@k8s-master01 ~]# kubectl get pods taint2 -n dev -o wide&#x000A;NAME                      READY   STATUS    RESTARTS   AGE     IP            NODE&#x000A;taint1-7665f7fd85-574h4   1/1     Running   0          2m24s   10.244.1.59   node1 &#x000A;taint2-544694789-6zmlf    0/1     Pending   0          21s     &lt;none&gt;        &lt;none&gt;   &#x000A;&#x000A;# 为node1设置污点(取消NoSchedule，设置NoExecute)&#x000A;[root@k8s-master01 ~]# kubectl taint nodes node1 tag:NoSchedule-&#x000A;[root@k8s-master01 ~]# kubectl taint nodes node1 tag=heima:NoExecute&#x000A;&#x000A;# 创建pod3&#x000A;[root@k8s-master01 ~]# kubectl run taint3 --image=nginx:1.17.1 -n dev&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -o wide&#x000A;NAME                      READY   STATUS    RESTARTS   AGE   IP       NODE     NOMINATED &#x000A;taint1-7665f7fd85-htkmp   0/1     Pending   0          35s   &lt;none&gt;   &lt;none&gt;   &lt;none&gt;    &#x000A;taint2-544694789-bn7wb    0/1     Pending   0          35s   &lt;none&gt;   &lt;none&gt;   &lt;none&gt;     &#x000A;taint3-6d78dbd749-tktkq   0/1     Pending   0          6s    &lt;none&gt;   &lt;none&gt;   &lt;none&gt;     &#x000A;```&#x000A;&#x000A;```&#x000A;小提示：&#x000A;    使用kubeadm搭建的集群，默认就会给master节点添加一个污点标记,所以pod就不会调度到master节点上.&#x000A;```&#x000A;&#x000A;**容忍（Toleration）**&#x000A;&#x000A;上面介绍了污点的作用，我们可以在node上添加污点用于拒绝pod调度上来，但是如果就是想将一个pod调度到一个有污点的node上去，这时候应该怎么做呢？这就要使用到**容忍**。&#x000A;&#x000A;![image-20200514095913741](Kubenetes.assets/image-20200514095913741.png)&#x000A;&#x000A;&gt; 污点就是拒绝，容忍就是忽略，Node通过污点拒绝pod调度上去，Pod通过容忍忽略拒绝&#x000A;&#x000A;下面先通过一个案例看下效果：&#x000A;&#x000A;1. 上一小节，已经在node1节点上打上了`NoExecute`的污点，此时pod是调度不上去的&#x000A;2. 本小节，可以通过给pod添加容忍，然后将其调度上去&#x000A;&#x000A;创建pod-toleration.yaml,内容如下&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-toleration&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  tolerations:      # 添加容忍&#x000A;  - key: &quot;tag&quot;        # 要容忍的污点的key&#x000A;    operator: &quot;Equal&quot; # 操作符&#x000A;    value: &quot;heima&quot;    # 容忍的污点的value&#x000A;    effect: &quot;NoExecute&quot;   # 添加容忍的规则，这里必须和标记的污点规则相同&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 添加容忍之前的pod&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -o wide&#x000A;NAME             READY   STATUS    RESTARTS   AGE   IP       NODE     NOMINATED &#x000A;pod-toleration   0/1     Pending   0          3s    &lt;none&gt;   &lt;none&gt;   &lt;none&gt;           &#x000A;&#x000A;# 添加容忍之后的pod&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -o wide&#x000A;NAME             READY   STATUS    RESTARTS   AGE   IP            NODE    NOMINATED&#x000A;pod-toleration   1/1     Running   0          3s    10.244.1.62   node1   &lt;none&gt;        &#x000A;```&#x000A;&#x000A;下面看一下容忍的详细配置:&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# kubectl explain pod.spec.tolerations&#x000A;......&#x000A;FIELDS:&#x000A;   key       # 对应着要容忍的污点的键，空意味着匹配所有的键&#x000A;   value     # 对应着要容忍的污点的值&#x000A;   operator  # key-value的运算符，支持Equal和Exists（默认）&#x000A;   effect    # 对应污点的effect，空意味着匹配所有影响&#x000A;   tolerationSeconds   # 容忍时间, 当effect为NoExecute时生效，表示pod在Node上的停留时间&#x000A;```&#x000A;&#x000A; &#x000A;&#x000A;### 6. Pod控制器详解&#x000A;&#x000A;#### 6.1 Pod控制器介绍&#x000A;&#x000A;Pod是kubernetes的最小管理单元，在kubernetes中，按照pod的创建方式可以将其分为两类：&#x000A;&#x000A;- 自主式pod：kubernetes直接创建出来的Pod，这种pod删除后就没有了，也不会重建&#x000A;- 控制器创建的pod：kubernetes通过控制器创建的pod，这种pod删除了之后还会自动重建&#x000A;&#x000A;&gt; **`什么是Pod控制器`**&#x000A;&gt;&#x000A;&gt; Pod控制器是管理pod的中间层，使用Pod控制器之后，只需要告诉Pod控制器，想要多少个什么样的Pod就可以了，它会创建出满足条件的Pod并确保每一个Pod资源处于用户期望的目标状态。如果Pod资源在运行中出现故障，它会基于指定策略重新编排Pod。&#x000A;&#x000A;在kubernetes中，有很多类型的pod控制器，每种都有自己的适合的场景，常见的有下面这些：&#x000A;&#x000A;- ReplicationController：比较原始的pod控制器，已经被废弃，由ReplicaSet替代&#x000A;- ReplicaSet：保证副本数量一直维持在期望值，并支持pod数量扩缩容，镜像版本升级&#x000A;- Deployment：通过控制ReplicaSet来控制Pod，并支持滚动升级、回退版本&#x000A;- Horizontal Pod Autoscaler：可以根据集群负载自动水平调整Pod的数量，实现削峰填谷&#x000A;- DaemonSet：在集群中的指定Node上运行且仅运行一个副本，一般用于守护进程类的任务&#x000A;- Job：它创建出来的pod只要完成任务就立即退出，不需要重启或重建，用于执行一次性任务&#x000A;- Cronjob：它创建的Pod负责周期性任务控制，不需要持续后台运行&#x000A;- StatefulSet：管理有状态应用&#x000A;&#x000A;#### 6.2 ReplicaSet(RS)&#x000A;&#x000A;ReplicaSet的主要作用是**保证一定数量的pod正常运行**，它会持续监听这些Pod的运行状态，一旦Pod发生故障，就会重启或重建。同时它还支持对pod数量的扩缩容和镜像版本的升降级。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200612005334159.png)&#x000A;&#x000A;ReplicaSet的资源清单文件：&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1 # 版本号&#x000A;kind: ReplicaSet # 类型       &#x000A;metadata: # 元数据&#x000A;  name: # rs名称 &#x000A;  namespace: # 所属命名空间 &#x000A;  labels: #标签&#x000A;    controller: rs&#x000A;spec: # 详情描述&#x000A;  replicas: 3 # 副本数量&#x000A;  selector: # 选择器，通过它指定该控制器管理哪些pod&#x000A;    matchLabels:      # Labels匹配规则&#x000A;      app: nginx-pod&#x000A;    matchExpressions: # Expressions匹配规则&#x000A;      - {key: app, operator: In, values: [nginx-pod]}&#x000A;  template: # 模板，当副本数量不足时，会根据下面的模板创建pod副本&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: nginx-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: nginx&#x000A;        image: nginx:1.17.1&#x000A;        ports:&#x000A;        - containerPort: 80&#x000A;```&#x000A;&#x000A;在这里面，需要新了解的配置项就是`spec`下面几个选项：&#x000A;&#x000A;- replicas：指定副本数量，其实就是当前rs创建出来的pod的数量，默认为1&#x000A;&#x000A;- selector：选择器，它的作用是建立pod控制器和pod之间的关联关系，采用的Label Selector机制&#x000A;&#x000A;  在pod模板上定义label，在控制器上定义选择器，就可以表明当前控制器能管理哪些pod了&#x000A;&#x000A;- template：模板，就是当前控制器创建pod所使用的模板板，里面其实就是前一章学过的pod的定义&#x000A;&#x000A;**创建ReplicaSet**&#x000A;&#x000A;创建pc-replicaset.yaml文件，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1&#x000A;kind: ReplicaSet   &#x000A;metadata:&#x000A;  name: pc-replicaset&#x000A;  namespace: dev&#x000A;spec:&#x000A;  replicas: 3&#x000A;  selector: &#x000A;    matchLabels:&#x000A;      app: nginx-pod&#x000A;  template:&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: nginx-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: nginx&#x000A;        image: nginx:1.17.1&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建rs&#x000A;[root@k8s-master01 ~]# kubectl create -f pc-replicaset.yaml&#x000A;replicaset.apps/pc-replicaset created&#x000A;&#x000A;# 查看rs&#x000A;# DESIRED:期望副本数量  &#x000A;# CURRENT:当前副本数量  &#x000A;# READY:已经准备好提供服务的副本数量&#x000A;[root@k8s-master01 ~]# kubectl get rs pc-replicaset -n dev -o wide&#x000A;NAME          DESIRED   CURRENT READY AGE   CONTAINERS   IMAGES             SELECTOR&#x000A;pc-replicaset 3         3       3     22s   nginx        nginx:1.17.1       app=nginx-pod&#x000A;&#x000A;# 查看当前控制器创建出来的pod&#x000A;# 这里发现控制器创建出来的pod的名称是在控制器名称后面拼接了-xxxxx随机码&#x000A;[root@k8s-master01 ~]# kubectl get pod -n dev&#x000A;NAME                          READY   STATUS    RESTARTS   AGE&#x000A;pc-replicaset-6vmvt   1/1     Running   0          54s&#x000A;pc-replicaset-fmb8f   1/1     Running   0          54s&#x000A;pc-replicaset-snrk2   1/1     Running   0          54s&#x000A;```&#x000A;&#x000A;**扩缩容**&#x000A;&#x000A;```shell&#x000A;# 编辑rs的副本数量，修改spec:replicas: 6即可&#x000A;[root@k8s-master01 ~]# kubectl edit rs pc-replicaset -n dev&#x000A;replicaset.apps/pc-replicaset edited&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev&#x000A;NAME                          READY   STATUS    RESTARTS   AGE&#x000A;pc-replicaset-6vmvt   1/1     Running   0          114m&#x000A;pc-replicaset-cftnp   1/1     Running   0          10s&#x000A;pc-replicaset-fjlm6   1/1     Running   0          10s&#x000A;pc-replicaset-fmb8f   1/1     Running   0          114m&#x000A;pc-replicaset-s2whj   1/1     Running   0          10s&#x000A;pc-replicaset-snrk2   1/1     Running   0          114m&#x000A;&#x000A;# 当然也可以直接使用命令实现&#x000A;# 使用scale命令实现扩缩容， 后面--replicas=n直接指定目标数量即可&#x000A;[root@k8s-master01 ~]# kubectl scale rs pc-replicaset --replicas=2 -n dev&#x000A;replicaset.apps/pc-replicaset scaled&#x000A;&#x000A;# 命令运行完毕，立即查看，发现已经有4个开始准备退出了&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev&#x000A;NAME                       READY   STATUS        RESTARTS   AGE&#x000A;pc-replicaset-6vmvt   0/1     Terminating   0          118m&#x000A;pc-replicaset-cftnp   0/1     Terminating   0          4m17s&#x000A;pc-replicaset-fjlm6   0/1     Terminating   0          4m17s&#x000A;pc-replicaset-fmb8f   1/1     Running       0          118m&#x000A;pc-replicaset-s2whj   0/1     Terminating   0          4m17s&#x000A;pc-replicaset-snrk2   1/1     Running       0          118m&#x000A;&#x000A;#稍等片刻，就只剩下2个了&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev&#x000A;NAME                       READY   STATUS    RESTARTS   AGE&#x000A;pc-replicaset-fmb8f   1/1     Running   0          119m&#x000A;pc-replicaset-snrk2   1/1     Running   0          119m&#x000A;```&#x000A;&#x000A;**镜像升级**&#x000A;&#x000A;```shell&#x000A;# 编辑rs的容器镜像 - image: nginx:1.17.2&#x000A;[root@k8s-master01 ~]# kubectl edit rs pc-replicaset -n dev&#x000A;replicaset.apps/pc-replicaset edited&#x000A;&#x000A;# 再次查看，发现镜像版本已经变更了&#x000A;[root@k8s-master01 ~]# kubectl get rs -n dev -o wide&#x000A;NAME                DESIRED  CURRENT   READY   AGE    CONTAINERS   IMAGES        ...&#x000A;pc-replicaset       2        2         2       140m   nginx         nginx:1.17.2  ...&#x000A;&#x000A;# 同样的道理，也可以使用命令完成这个工作&#x000A;# kubectl set image rs rs名称 容器=镜像版本 -n namespace&#x000A;[root@k8s-master01 ~]# kubectl set image rs pc-replicaset nginx=nginx:1.17.1  -n dev&#x000A;replicaset.apps/pc-replicaset image updated&#x000A;&#x000A;# 再次查看，发现镜像版本已经变更了&#x000A;[root@k8s-master01 ~]# kubectl get rs -n dev -o wide&#x000A;NAME                 DESIRED  CURRENT   READY   AGE    CONTAINERS   IMAGES            ...&#x000A;pc-replicaset        2        2         2       145m   nginx        nginx:1.17.1 ... &#x000A;```&#x000A;&#x000A;**删除ReplicaSet**&#x000A;&#x000A;```shell&#x000A;# 使用kubectl delete命令会删除此RS以及它管理的Pod&#x000A;# 在kubernetes删除RS前，会将RS的replicasclear调整为0，等待所有的Pod被删除后，在执行RS对象的删除&#x000A;[root@k8s-master01 ~]# kubectl delete rs pc-replicaset -n dev&#x000A;replicaset.apps &quot;pc-replicaset&quot; deleted&#x000A;[root@k8s-master01 ~]# kubectl get pod -n dev -o wide&#x000A;No resources found in dev namespace.&#x000A;&#x000A;# 如果希望仅仅删除RS对象（保留Pod），可以使用kubectl delete命令时添加--cascade=false选项（不推荐）。&#x000A;[root@k8s-master01 ~]# kubectl delete rs pc-replicaset -n dev --cascade=false&#x000A;replicaset.apps &quot;pc-replicaset&quot; deleted&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev&#x000A;NAME                  READY   STATUS    RESTARTS   AGE&#x000A;pc-replicaset-cl82j   1/1     Running   0          75s&#x000A;pc-replicaset-dslhb   1/1     Running   0          75s&#x000A;&#x000A;# 也可以使用yaml直接删除(推荐)&#x000A;[root@k8s-master01 ~]# kubectl delete -f pc-replicaset.yaml&#x000A;replicaset.apps &quot;pc-replicaset&quot; deleted&#x000A;```&#x000A;&#x000A;#### 6.3 Deployment(Deploy)&#x000A;&#x000A;为了更好的解决服务编排的问题，kubernetes在V1.2版本开始，引入了Deployment控制器。值得一提的是，这种控制器并不直接管理pod，而是通过管理ReplicaSet来简介管理Pod，即：Deployment管理ReplicaSet，ReplicaSet管理Pod。所以Deployment比ReplicaSet功能更加强大。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200612005524778.png)&#x000A;&#x000A;Deployment主要功能有下面几个：&#x000A;&#x000A;- 支持ReplicaSet的所有功能&#x000A;- 支持发布的停止、继续&#x000A;- 支持滚动升级和回滚版本&#x000A;&#x000A;Deployment的资源清单文件：&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1 # 版本号&#x000A;kind: Deployment # 类型       &#x000A;metadata: # 元数据&#x000A;  name: # rs名称 &#x000A;  namespace: # 所属命名空间 &#x000A;  labels: #标签&#x000A;    controller: deploy&#x000A;spec: # 详情描述&#x000A;  replicas: 3 # 副本数量&#x000A;  revisionHistoryLimit: 3 # 保留历史版本&#x000A;  paused: false # 暂停部署，默认是false&#x000A;  progressDeadlineSeconds: 600 # 部署超时时间（s），默认是600&#x000A;  strategy: # 策略&#x000A;    type: RollingUpdate # 滚动更新策略&#x000A;    rollingUpdate: # 滚动更新&#x000A;      max违规词汇: 30% # 最大额外可以存在的副本数，可以为百分比，也可以为整数&#x000A;      maxUnavailable: 30% # 最大不可用状态的 Pod 的最大值，可以为百分比，也可以为整数&#x000A;  selector: # 选择器，通过它指定该控制器管理哪些pod&#x000A;    matchLabels:      # Labels匹配规则&#x000A;      app: nginx-pod&#x000A;    matchExpressions: # Expressions匹配规则&#x000A;      - {key: app, operator: In, values: [nginx-pod]}&#x000A;  template: # 模板，当副本数量不足时，会根据下面的模板创建pod副本&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: nginx-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: nginx&#x000A;        image: nginx:1.17.1&#x000A;        ports:&#x000A;        - containerPort: 80&#x000A;```&#x000A;&#x000A;##### 6.3.1 创建deployment&#x000A;&#x000A;创建pc-deployment.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1&#x000A;kind: Deployment      &#x000A;metadata:&#x000A;  name: pc-deployment&#x000A;  namespace: dev&#x000A;spec: &#x000A;  replicas: 3&#x000A;  selector:&#x000A;    matchLabels:&#x000A;      app: nginx-pod&#x000A;  template:&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: nginx-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: nginx&#x000A;        image: nginx:1.17.1&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建deployment&#x000A;[root@k8s-master01 ~]# kubectl create -f pc-deployment.yaml --record=true&#x000A;deployment.apps/pc-deployment created&#x000A;&#x000A;# 查看deployment&#x000A;# UP-TO-DATE 最新版本的pod的数量&#x000A;# AVAILABLE  当前可用的pod的数量&#x000A;[root@k8s-master01 ~]# kubectl get deploy pc-deployment -n dev&#x000A;NAME            READY   UP-TO-DATE   AVAILABLE   AGE&#x000A;pc-deployment   3/3     3            3           15s&#x000A;&#x000A;# 查看rs&#x000A;# 发现rs的名称是在原来deployment的名字后面添加了一个10位数的随机串&#x000A;[root@k8s-master01 ~]# kubectl get rs -n dev&#x000A;NAME                       DESIRED   CURRENT   READY   AGE&#x000A;pc-deployment-6696798b78   3         3         3       23s&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev&#x000A;NAME                             READY   STATUS    RESTARTS   AGE&#x000A;pc-deployment-6696798b78-d2c8n   1/1     Running   0          107s&#x000A;pc-deployment-6696798b78-smpvp   1/1     Running   0          107s&#x000A;pc-deployment-6696798b78-wvjd8   1/1     Running   0          107s&#x000A;```&#x000A;&#x000A;##### 6.3.2 扩缩容&#x000A;&#x000A;```shell&#x000A;# 变更副本数量为5个&#x000A;[root@k8s-master01 ~]# kubectl scale deploy pc-deployment --replicas=5  -n dev&#x000A;deployment.apps/pc-deployment scaled&#x000A;&#x000A;# 查看deployment&#x000A;[root@k8s-master01 ~]# kubectl get deploy pc-deployment -n dev&#x000A;NAME            READY   UP-TO-DATE   AVAILABLE   AGE&#x000A;pc-deployment   5/5     5            5           2m&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]#  kubectl get pods -n dev&#x000A;NAME                             READY   STATUS    RESTARTS   AGE&#x000A;pc-deployment-6696798b78-d2c8n   1/1     Running   0          4m19s&#x000A;pc-deployment-6696798b78-jxmdq   1/1     Running   0          94s&#x000A;pc-deployment-6696798b78-mktqv   1/1     Running   0          93s&#x000A;pc-deployment-6696798b78-smpvp   1/1     Running   0          4m19s&#x000A;pc-deployment-6696798b78-wvjd8   1/1     Running   0          4m19s&#x000A;&#x000A;# 编辑deployment的副本数量，修改spec:replicas: 4即可&#x000A;[root@k8s-master01 ~]# kubectl edit deploy pc-deployment -n dev&#x000A;deployment.apps/pc-deployment edited&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev&#x000A;NAME                             READY   STATUS    RESTARTS   AGE&#x000A;pc-deployment-6696798b78-d2c8n   1/1     Running   0          5m23s&#x000A;pc-deployment-6696798b78-jxmdq   1/1     Running   0          2m38s&#x000A;pc-deployment-6696798b78-smpvp   1/1     Running   0          5m23s&#x000A;pc-deployment-6696798b78-wvjd8   1/1     Running   0          5m23s&#x000A;```&#x000A;&#x000A;**镜像更新**&#x000A;&#x000A;deployment支持两种更新策略:`重建更新`和`滚动更新`,可以通过`strategy`指定策略类型,支持两个属性:&#x000A;&#x000A;```markdown&#x000A;strategy：指定新的Pod替换旧的Pod的策略， 支持两个属性：&#x000A;  type：指定策略类型，支持两种策略&#x000A;    Recreate：在创建出新的Pod之前会先杀掉所有已存在的Pod&#x000A;    RollingUpdate：滚动更新，就是杀死一部分，就启动一部分，在更新过程中，存在两个版本Pod&#x000A;  rollingUpdate：当type为RollingUpdate时生效，用于为RollingUpdate设置参数，支持两个属性：&#x000A;    maxUnavailable：用来指定在升级过程中不可用Pod的最大数量，默认为25%。&#x000A;    max违规词汇： 用来指定在升级过程中可以超过期望的Pod的最大数量，默认为25%。&#x000A;```&#x000A;&#x000A;重建更新&#x000A;&#x000A;1) 编辑pc-deployment.yaml,在spec节点下添加更新策略&#x000A;&#x000A;```yaml&#x000A;spec:&#x000A;  strategy: # 策略&#x000A;    type: Recreate # 重建更新&#x000A;```&#x000A;&#x000A;2) 创建deploy进行验证&#x000A;&#x000A;```shell&#x000A;# 变更镜像&#x000A;[root@k8s-master01 ~]# kubectl set image deployment pc-deployment nginx=nginx:1.17.2 -n dev&#x000A;deployment.apps/pc-deployment image updated&#x000A;&#x000A;# 观察升级过程&#x000A;[root@k8s-master01 ~]#  kubectl get pods -n dev -w&#x000A;NAME                             READY   STATUS    RESTARTS   AGE&#x000A;pc-deployment-5d89bdfbf9-65qcw   1/1     Running   0          31s&#x000A;pc-deployment-5d89bdfbf9-w5nzv   1/1     Running   0          31s&#x000A;pc-deployment-5d89bdfbf9-xpt7w   1/1     Running   0          31s&#x000A;&#x000A;pc-deployment-5d89bdfbf9-xpt7w   1/1     Terminating   0          41s&#x000A;pc-deployment-5d89bdfbf9-65qcw   1/1     Terminating   0          41s&#x000A;pc-deployment-5d89bdfbf9-w5nzv   1/1     Terminating   0          41s&#x000A;&#x000A;pc-deployment-675d469f8b-grn8z   0/1     Pending       0          0s&#x000A;pc-deployment-675d469f8b-hbl4v   0/1     Pending       0          0s&#x000A;pc-deployment-675d469f8b-67nz2   0/1     Pending       0          0s&#x000A;&#x000A;pc-deployment-675d469f8b-grn8z   0/1     ContainerCreating   0          0s&#x000A;pc-deployment-675d469f8b-hbl4v   0/1     ContainerCreating   0          0s&#x000A;pc-deployment-675d469f8b-67nz2   0/1     ContainerCreating   0          0s&#x000A;&#x000A;pc-deployment-675d469f8b-grn8z   1/1     Running             0          1s&#x000A;pc-deployment-675d469f8b-67nz2   1/1     Running             0          1s&#x000A;pc-deployment-675d469f8b-hbl4v   1/1     Running             0          2s&#x000A;```&#x000A;&#x000A;滚动更新&#x000A;&#x000A;1) 编辑pc-deployment.yaml,在spec节点下添加更新策略&#x000A;&#x000A;```yaml&#x000A;spec:&#x000A;  strategy: # 策略&#x000A;    type: RollingUpdate # 滚动更新策略&#x000A;    rollingUpdate:&#x000A;      max违规词汇: 25% &#x000A;      maxUnavailable: 25%&#x000A;```&#x000A;&#x000A;2) 创建deploy进行验证&#x000A;&#x000A;```shell&#x000A;# 变更镜像&#x000A;[root@k8s-master01 ~]# kubectl set image deployment pc-deployment nginx=nginx:1.17.3 -n dev &#x000A;deployment.apps/pc-deployment image updated&#x000A;&#x000A;# 观察升级过程&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -w&#x000A;NAME                           READY   STATUS    RESTARTS   AGE&#x000A;pc-deployment-c848d767-8rbzt   1/1     Running   0          31m&#x000A;pc-deployment-c848d767-h4p68   1/1     Running   0          31m&#x000A;pc-deployment-c848d767-hlmz4   1/1     Running   0          31m&#x000A;pc-deployment-c848d767-rrqcn   1/1     Running   0          31m&#x000A;&#x000A;pc-deployment-966bf7f44-226rx   0/1     Pending             0          0s&#x000A;pc-deployment-966bf7f44-226rx   0/1     ContainerCreating   0          0s&#x000A;pc-deployment-966bf7f44-226rx   1/1     Running             0          1s&#x000A;pc-deployment-c848d767-h4p68    0/1     Terminating         0          34m&#x000A;&#x000A;pc-deployment-966bf7f44-cnd44   0/1     Pending             0          0s&#x000A;pc-deployment-966bf7f44-cnd44   0/1     ContainerCreating   0          0s&#x000A;pc-deployment-966bf7f44-cnd44   1/1     Running             0          2s&#x000A;pc-deployment-c848d767-hlmz4    0/1     Terminating         0          34m&#x000A;&#x000A;pc-deployment-966bf7f44-px48p   0/1     Pending             0          0s&#x000A;pc-deployment-966bf7f44-px48p   0/1     ContainerCreating   0          0s&#x000A;pc-deployment-966bf7f44-px48p   1/1     Running             0          0s&#x000A;pc-deployment-c848d767-8rbzt    0/1     Terminating         0          34m&#x000A;&#x000A;pc-deployment-966bf7f44-dkmqp   0/1     Pending             0          0s&#x000A;pc-deployment-966bf7f44-dkmqp   0/1     ContainerCreating   0          0s&#x000A;pc-deployment-966bf7f44-dkmqp   1/1     Running             0          2s&#x000A;pc-deployment-c848d767-rrqcn    0/1     Terminating         0          34m&#x000A;&#x000A;# 至此，新版本的pod创建完毕，就版本的pod销毁完毕&#x000A;# 中间过程是滚动进行的，也就是边销毁边创建&#x000A;```&#x000A;&#x000A;滚动更新的过程：&#x000A;&#x000A;![img](Kubenetes.assets/image-20200416140251491.png)&#x000A;&#x000A;镜像更新中rs的变化&#x000A;&#x000A;```shell&#x000A;# 查看rs,发现原来的rs的依旧存在，只是pod数量变为了0，而后又新产生了一个rs，pod数量为4&#x000A;# 其实这就是deployment能够进行版本回退的奥妙所在，后面会详细解释&#x000A;[root@k8s-master01 ~]# kubectl get rs -n dev&#x000A;NAME                       DESIRED   CURRENT   READY   AGE&#x000A;pc-deployment-6696798b78   0         0         0       7m37s&#x000A;pc-deployment-6696798b11   0         0         0       5m37s&#x000A;pc-deployment-c848d76789   4         4         4       72s&#x000A;```&#x000A;&#x000A;##### 6.3.3 版本回退&#x000A;&#x000A;deployment支持版本升级过程中的暂停、继续功能以及版本回退等诸多功能，下面具体来看.&#x000A;&#x000A;kubectl rollout： 版本升级相关功能，支持下面的选项：&#x000A;&#x000A;- status	显示当前升级状态&#x000A;- history   显示 升级历史记录&#x000A;- pause    暂停版本升级过程&#x000A;- resume   继续已经暂停的版本升级过程&#x000A;- restart    重启版本升级过程&#x000A;- undo 回滚到上一级版本（可以使用--to-revision回滚到指定版本）&#x000A;&#x000A;```shell&#x000A;# 查看当前升级版本的状态&#x000A;[root@k8s-master01 ~]# kubectl rollout status deploy pc-deployment -n dev&#x000A;deployment &quot;pc-deployment&quot; successfully rolled out&#x000A;&#x000A;# 查看升级历史记录&#x000A;[root@k8s-master01 ~]# kubectl rollout history deploy pc-deployment -n dev&#x000A;deployment.apps/pc-deployment&#x000A;REVISION  CHANGE-CAUSE&#x000A;1         kubectl create --filename=pc-deployment.yaml --record=true&#x000A;2         kubectl create --filename=pc-deployment.yaml --record=true&#x000A;3         kubectl create --filename=pc-deployment.yaml --record=true&#x000A;# 可以发现有三次版本记录，说明完成过两次升级&#x000A;&#x000A;# 版本回滚&#x000A;# 这里直接使用--to-revision=1回滚到了1版本， 如果省略这个选项，就是回退到上个版本，就是2版本&#x000A;[root@k8s-master01 ~]# kubectl rollout undo deployment pc-deployment --to-revision=1 -n dev&#x000A;deployment.apps/pc-deployment rolled back&#x000A;&#x000A;# 查看发现，通过nginx镜像版本可以发现到了第一版&#x000A;[root@k8s-master01 ~]# kubectl get deploy -n dev -o wide&#x000A;NAME            READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES         &#x000A;pc-deployment   4/4     4            4           74m   nginx        nginx:1.17.1   &#x000A;&#x000A;# 查看rs，发现第一个rs中有4个pod运行，后面两个版本的rs中pod为运行&#x000A;# 其实deployment之所以可是实现版本的回滚，就是通过记录下历史rs来实现的，&#x000A;# 一旦想回滚到哪个版本，只需要将当前版本pod数量降为0，然后将回滚版本的pod提升为目标数量就可以了&#x000A;[root@k8s-master01 ~]# kubectl get rs -n dev&#x000A;NAME                       DESIRED   CURRENT   READY   AGE&#x000A;pc-deployment-6696798b78   4         4         4       78m&#x000A;pc-deployment-966bf7f44    0         0         0       37m&#x000A;pc-deployment-c848d767     0         0         0       71m&#x000A;```&#x000A;&#x000A;##### 6.3.4 金丝雀发布&#x000A;&#x000A;Deployment控制器支持控制更新过程中的控制，如“暂停(pause)”或“继续(resume)”更新操作。&#x000A;&#x000A;比如有一批新的Pod资源创建完成后立即暂停更新过程，此时，仅存在一部分新版本的应用，主体部分还是旧的版本。然后，再筛选一小部分的用户请求路由到新版本的Pod应用，继续观察能否稳定地按期望的方式运行。确定没问题之后再继续完成余下的Pod资源滚动更新，否则立即回滚更新操作。这就是所谓的金丝雀发布。&#x000A;&#x000A;```shell&#x000A;# 更新deployment的版本，并配置暂停deployment&#x000A;[root@k8s-master01 ~]#  kubectl set image deploy pc-deployment nginx=nginx:1.17.4 -n dev &amp;&amp; kubectl rollout pause deployment pc-deployment  -n dev&#x000A;deployment.apps/pc-deployment image updated&#x000A;deployment.apps/pc-deployment paused&#x000A;&#x000A;#观察更新状态&#x000A;[root@k8s-master01 ~]# kubectl rollout status deploy pc-deployment -n dev　&#x000A;Waiting for deployment &quot;pc-deployment&quot; rollout to finish: 2 out of 4 new replicas have been updated...&#x000A;&#x000A;# 监控更新的过程，可以看到已经新增了一个资源，但是并未按照预期的状态去删除一个旧的资源，就是因为使用了pause暂停命令&#x000A;&#x000A;[root@k8s-master01 ~]# kubectl get rs -n dev -o wide&#x000A;NAME                       DESIRED   CURRENT   READY   AGE     CONTAINERS   IMAGES         &#x000A;pc-deployment-5d89bdfbf9   3         3         3       19m     nginx        nginx:1.17.1   &#x000A;pc-deployment-675d469f8b   0         0         0       14m     nginx        nginx:1.17.2   &#x000A;pc-deployment-6c9f56fcfb   2         2         2       3m16s   nginx        nginx:1.17.4   &#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev&#x000A;NAME                             READY   STATUS    RESTARTS   AGE&#x000A;pc-deployment-5d89bdfbf9-rj8sq   1/1     Running   0          7m33s&#x000A;pc-deployment-5d89bdfbf9-ttwgg   1/1     Running   0          7m35s&#x000A;pc-deployment-5d89bdfbf9-v4wvc   1/1     Running   0          7m34s&#x000A;pc-deployment-6c9f56fcfb-996rt   1/1     Running   0          3m31s&#x000A;pc-deployment-6c9f56fcfb-j2gtj   1/1     Running   0          3m31s&#x000A;&#x000A;# 确保更新的pod没问题了，继续更新&#x000A;[root@k8s-master01 ~]# kubectl rollout resume deploy pc-deployment -n dev&#x000A;deployment.apps/pc-deployment resumed&#x000A;&#x000A;# 查看最后的更新情况&#x000A;[root@k8s-master01 ~]# kubectl get rs -n dev -o wide&#x000A;NAME                       DESIRED   CURRENT   READY   AGE     CONTAINERS   IMAGES         &#x000A;pc-deployment-5d89bdfbf9   0         0         0       21m     nginx        nginx:1.17.1   &#x000A;pc-deployment-675d469f8b   0         0         0       16m     nginx        nginx:1.17.2   &#x000A;pc-deployment-6c9f56fcfb   4         4         4       5m11s   nginx        nginx:1.17.4   &#x000A;&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev&#x000A;NAME                             READY   STATUS    RESTARTS   AGE&#x000A;pc-deployment-6c9f56fcfb-7bfwh   1/1     Running   0          37s&#x000A;pc-deployment-6c9f56fcfb-996rt   1/1     Running   0          5m27s&#x000A;pc-deployment-6c9f56fcfb-j2gtj   1/1     Running   0          5m27s&#x000A;pc-deployment-6c9f56fcfb-rf84v   1/1     Running   0          37s&#x000A;```&#x000A;&#x000A;**删除Deployment**&#x000A;&#x000A;```shell&#x000A;# 删除deployment，其下的rs和pod也将被删除&#x000A;[root@k8s-master01 ~]# kubectl delete -f pc-deployment.yaml&#x000A;deployment.apps &quot;pc-deployment&quot; deleted&#x000A;```&#x000A;&#x000A;#### 6.4 Horizontal Pod Autoscaler(HPA)&#x000A;&#x000A;在前面的课程中，我们已经可以实现通过手工执行`kubectl scale`命令实现Pod扩容或缩容，但是这显然不符合Kubernetes的定位目标--自动化、智能化。 Kubernetes期望可以实现通过监测Pod的使用情况，实现pod数量的自动调整，于是就产生了Horizontal Pod Autoscaler（HPA）这种控制器。&#x000A;&#x000A;HPA可以获取每个Pod利用率，然后和HPA中定义的指标进行对比，同时计算出需要伸缩的具体值，最后实现Pod的数量的调整。其实HPA与之前的Deployment一样，也属于一种Kubernetes资源对象，它通过追踪分析RC控制的所有目标Pod的负载变化情况，来确定是否需要针对性地调整目标Pod的副本数，这是HPA的实现原理。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200608155858271.png)&#x000A;&#x000A;接下来，我们来做一个实验&#x000A;&#x000A;##### 6.4.1 安装metrics-server&#x000A;&#x000A;metrics-server可以用来收集集群中的资源使用情况&#x000A;&#x000A;```shell&#x000A;# 安装git&#x000A;[root@k8s-master01 ~]# yum install git -y&#x000A;# 获取metrics-server, 注意使用的版本&#x000A;[root@k8s-master01 ~]# git clone -b v0.3.6 https://github.com/kubernetes-incubator/metrics-server&#x000A;# 修改deployment, 注意修改的是镜像和初始化参数&#x000A;[root@k8s-master01 ~]# cd /root/metrics-server/deploy/1.8+/&#x000A;[root@k8s-master01 1.8+]# vim metrics-server-deployment.yaml&#x000A;按图中添加下面选项&#x000A;hostNetwork: true&#x000A;image: registry.cn-hangzhou.aliyuncs.com/google_containers/metrics-server-amd64:v0.3.6&#x000A;args:&#x000A;- --kubelet-insecure-tls&#x000A;- --kubelet-preferred-address-types=InternalIP,Hostname,InternalDNS,ExternalDNS,ExternalIP&#x000A;```&#x000A;&#x000A;![image-20200608163326496](Kubenetes.assets/image-20200608163326496.png)&#x000A;&#x000A;```shell&#x000A;# 安装metrics-server&#x000A;[root@k8s-master01 1.8+]# kubectl apply -f ./&#x000A;&#x000A;# 查看pod运行情况&#x000A;[root@k8s-master01 1.8+]# kubectl get pod -n kube-system&#x000A;metrics-server-6b976979db-2xwbj   1/1     Running   0          90s&#x000A;&#x000A;# 使用kubectl top node 查看资源使用情况&#x000A;[root@k8s-master01 1.8+]# kubectl top node&#x000A;NAME           CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%&#x000A;k8s-master01   289m         14%    1582Mi          54%       &#x000A;k8s-node01     81m          4%     1195Mi          40%       &#x000A;k8s-node02     72m          3%     1211Mi          41%  &#x000A;[root@k8s-master01 1.8+]# kubectl top pod -n kube-system&#x000A;NAME                              CPU(cores)   MEMORY(bytes)&#x000A;coredns-6955765f44-7ptsb          3m           9Mi&#x000A;coredns-6955765f44-vcwr5          3m           8Mi&#x000A;etcd-master                       14m          145Mi&#x000A;...&#x000A;# 至此,metrics-server安装完成&#x000A;```&#x000A;&#x000A;##### 6.4.2 准备deployment和servie&#x000A;&#x000A;创建pc-hpa-pod.yaml文件，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1&#x000A;kind: Deployment&#x000A;metadata:&#x000A;  name: nginx&#x000A;  namespace: dev&#x000A;spec:&#x000A;  strategy: # 策略&#x000A;    type: RollingUpdate # 滚动更新策略&#x000A;  replicas: 1&#x000A;  selector:&#x000A;    matchLabels:&#x000A;      app: nginx-pod&#x000A;  template:&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: nginx-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: nginx&#x000A;        image: nginx:1.17.1&#x000A;        resources: # 资源配额&#x000A;          limits:  # 限制资源（上限）&#x000A;            cpu: &quot;1&quot; # CPU限制，单位是core数&#x000A;          requests: # 请求资源（下限）&#x000A;            cpu: &quot;100m&quot;  # CPU限制，单位是core数&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建deployment&#x000A;[root@k8s-master01 1.8+]# kubectl run nginx --image=nginx:1.17.1 --requests=cpu=100m -n dev&#x000A;# 创建service&#x000A;[root@k8s-master01 1.8+]# kubectl expose deployment nginx --type=NodePort --port=80 -n dev&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 查看&#x000A;[root@k8s-master01 1.8+]# kubectl get deployment,pod,svc -n dev&#x000A;NAME                    READY   UP-TO-DATE   AVAILABLE   AGE&#x000A;deployment.apps/nginx   1/1     1            1           47s&#x000A;&#x000A;NAME                         READY   STATUS    RESTARTS   AGE&#x000A;pod/nginx-7df9756ccc-bh8dr   1/1     Running   0          47s&#x000A;&#x000A;NAME            TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE&#x000A;service/nginx   NodePort   10.101.18.29   &lt;none&gt;        80:31830/TCP   35s&#x000A;```&#x000A;&#x000A;##### 6.4.3 部署HPA&#x000A;&#x000A;创建pc-hpa.yaml文件，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: autoscaling/v1&#x000A;kind: HorizontalPodAutoscaler&#x000A;metadata:&#x000A;  name: pc-hpa&#x000A;  namespace: dev&#x000A;spec:&#x000A;  minReplicas: 1  #最小pod数量&#x000A;  maxReplicas: 10 #最大pod数量&#x000A;  targetCPUUtilizationPercentage: 3 # CPU使用率指标&#x000A;  scaleTargetRef:   # 指定要控制的nginx信息&#x000A;    apiVersion:  apps/v1&#x000A;    kind: Deployment&#x000A;    name: nginx&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建hpa&#x000A;[root@k8s-master01 1.8+]# kubectl create -f pc-hpa.yaml&#x000A;horizontalpodautoscaler.autoscaling/pc-hpa created&#x000A;&#x000A;# 查看hpa&#x000A;    [root@k8s-master01 1.8+]# kubectl get hpa -n dev&#x000A;NAME     REFERENCE          TARGETS   MINPODS   MAXPODS   REPLICAS   AGE&#x000A;pc-hpa   Deployment/nginx   0%/3%     1         10        1          62s&#x000A;```&#x000A;&#x000A;##### 6.4.4 测试&#x000A;&#x000A;使用压测工具对service地址`192.168.5.4:31830`进行压测，然后通过控制台查看hpa和pod的变化&#x000A;&#x000A;hpa变化&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# kubectl get hpa -n dev -w&#x000A;NAME   REFERENCE      TARGETS  MINPODS  MAXPODS  REPLICAS  AGE&#x000A;pc-hpa  Deployment/nginx  0%/3%   1     10     1      4m11s&#x000A;pc-hpa  Deployment/nginx  0%/3%   1     10     1      5m19s&#x000A;pc-hpa  Deployment/nginx  22%/3%   1     10     1      6m50s&#x000A;pc-hpa  Deployment/nginx  22%/3%   1     10     4      7m5s&#x000A;pc-hpa  Deployment/nginx  22%/3%   1     10     8      7m21s&#x000A;pc-hpa  Deployment/nginx  6%/3%   1     10     8      7m51s&#x000A;pc-hpa  Deployment/nginx  0%/3%   1     10     8      9m6s&#x000A;pc-hpa  Deployment/nginx  0%/3%   1     10     8      13m&#x000A;pc-hpa  Deployment/nginx  0%/3%   1     10     1      14m&#x000A;```&#x000A;&#x000A;deployment变化&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# kubectl get deployment -n dev -w&#x000A;NAME    READY   UP-TO-DATE   AVAILABLE   AGE&#x000A;nginx   1/1     1            1           11m&#x000A;nginx   1/4     1            1           13m&#x000A;nginx   1/4     1            1           13m&#x000A;nginx   1/4     1            1           13m&#x000A;nginx   1/4     4            1           13m&#x000A;nginx   1/8     4            1           14m&#x000A;nginx   1/8     4            1           14m&#x000A;nginx   1/8     4            1           14m&#x000A;nginx   1/8     8            1           14m&#x000A;nginx   2/8     8            2           14m&#x000A;nginx   3/8     8            3           14m&#x000A;nginx   4/8     8            4           14m&#x000A;nginx   5/8     8            5           14m&#x000A;nginx   6/8     8            6           14m&#x000A;nginx   7/8     8            7           14m&#x000A;nginx   8/8     8            8           15m&#x000A;nginx   8/1     8            8           20m&#x000A;nginx   8/1     8            8           20m&#x000A;nginx   1/1     1            1           20m&#x000A;```&#x000A;&#x000A;pod变化&#x000A;&#x000A;```&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -w&#x000A;NAME                     READY   STATUS    RESTARTS   AGE&#x000A;nginx-7df9756ccc-bh8dr   1/1     Running   0          11m&#x000A;nginx-7df9756ccc-cpgrv   0/1     Pending   0          0s&#x000A;nginx-7df9756ccc-8zhwk   0/1     Pending   0          0s&#x000A;nginx-7df9756ccc-rr9bn   0/1     Pending   0          0s&#x000A;nginx-7df9756ccc-cpgrv   0/1     ContainerCreating   0          0s&#x000A;nginx-7df9756ccc-8zhwk   0/1     ContainerCreating   0          0s&#x000A;nginx-7df9756ccc-rr9bn   0/1     ContainerCreating   0          0s&#x000A;nginx-7df9756ccc-m9gsj   0/1     Pending             0          0s&#x000A;nginx-7df9756ccc-g56qb   0/1     Pending             0          0s&#x000A;nginx-7df9756ccc-sl9c6   0/1     Pending             0          0s&#x000A;nginx-7df9756ccc-fgst7   0/1     Pending             0          0s&#x000A;nginx-7df9756ccc-g56qb   0/1     ContainerCreating   0          0s&#x000A;nginx-7df9756ccc-m9gsj   0/1     ContainerCreating   0          0s&#x000A;nginx-7df9756ccc-sl9c6   0/1     ContainerCreating   0          0s&#x000A;nginx-7df9756ccc-fgst7   0/1     ContainerCreating   0          0s&#x000A;nginx-7df9756ccc-8zhwk   1/1     Running             0          19s&#x000A;nginx-7df9756ccc-rr9bn   1/1     Running             0          30s&#x000A;nginx-7df9756ccc-m9gsj   1/1     Running             0          21s&#x000A;nginx-7df9756ccc-cpgrv   1/1     Running             0          47s&#x000A;nginx-7df9756ccc-sl9c6   1/1     Running             0          33s&#x000A;nginx-7df9756ccc-g56qb   1/1     Running             0          48s&#x000A;nginx-7df9756ccc-fgst7   1/1     Running             0          66s&#x000A;nginx-7df9756ccc-fgst7   1/1     Terminating         0          6m50s&#x000A;nginx-7df9756ccc-8zhwk   1/1     Terminating         0          7m5s&#x000A;nginx-7df9756ccc-cpgrv   1/1     Terminating         0          7m5s&#x000A;nginx-7df9756ccc-g56qb   1/1     Terminating         0          6m50s&#x000A;nginx-7df9756ccc-rr9bn   1/1     Terminating         0          7m5s&#x000A;nginx-7df9756ccc-m9gsj   1/1     Terminating         0          6m50s&#x000A;nginx-7df9756ccc-sl9c6   1/1     Terminating         0          6m50s&#x000A;```&#x000A;&#x000A;#### 6.5 DaemonSet(DS)&#x000A;&#x000A;DaemonSet类型的控制器可以保证在集群中的每一台（或指定）节点上都运行一个副本。一般适用于日志收集、节点监控等场景。也就是说，如果一个Pod提供的功能是节点级别的（每个节点都需要且只需要一个），那么这类Pod就适合使用DaemonSet类型的控制器创建。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200612010223537.png)&#x000A;&#x000A;DaemonSet控制器的特点：&#x000A;&#x000A;- 每当向集群中添加一个节点时，指定的 Pod 副本也将添加到该节点上&#x000A;- 当节点从集群中移除时，Pod 也就被垃圾回收了&#x000A;&#x000A;下面先来看下DaemonSet的资源清单文件&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1 # 版本号&#x000A;kind: DaemonSet # 类型       &#x000A;metadata: # 元数据&#x000A;  name: # rs名称 &#x000A;  namespace: # 所属命名空间 &#x000A;  labels: #标签&#x000A;    controller: daemonset&#x000A;spec: # 详情描述&#x000A;  revisionHistoryLimit: 3 # 保留历史版本&#x000A;  updateStrategy: # 更新策略&#x000A;    type: RollingUpdate # 滚动更新策略&#x000A;    rollingUpdate: # 滚动更新&#x000A;      maxUnavailable: 1 # 最大不可用状态的 Pod 的最大值，可以为百分比，也可以为整数&#x000A;  selector: # 选择器，通过它指定该控制器管理哪些pod&#x000A;    matchLabels:      # Labels匹配规则&#x000A;      app: nginx-pod&#x000A;    matchExpressions: # Expressions匹配规则&#x000A;      - {key: app, operator: In, values: [nginx-pod]}&#x000A;  template: # 模板，当副本数量不足时，会根据下面的模板创建pod副本&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: nginx-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: nginx&#x000A;        image: nginx:1.17.1&#x000A;        ports:&#x000A;        - containerPort: 80&#x000A;```&#x000A;&#x000A;创建pc-daemonset.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1&#x000A;kind: DaemonSet      &#x000A;metadata:&#x000A;  name: pc-daemonset&#x000A;  namespace: dev&#x000A;spec: &#x000A;  selector:&#x000A;    matchLabels:&#x000A;      app: nginx-pod&#x000A;  template:&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: nginx-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: nginx&#x000A;        image: nginx:1.17.1&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建daemonset&#x000A;[root@k8s-master01 ~]# kubectl create -f  pc-daemonset.yaml&#x000A;daemonset.apps/pc-daemonset created&#x000A;&#x000A;# 查看daemonset&#x000A;[root@k8s-master01 ~]#  kubectl get ds -n dev -o wide&#x000A;NAME        DESIRED  CURRENT  READY  UP-TO-DATE  AVAILABLE   AGE   CONTAINERS   IMAGES         &#x000A;pc-daemonset   2        2        2      2           2        24s   nginx        nginx:1.17.1   &#x000A;&#x000A;# 查看pod,发现在每个Node上都运行一个pod&#x000A;[root@k8s-master01 ~]#  kubectl get pods -n dev -o wide&#x000A;NAME                 READY   STATUS    RESTARTS   AGE   IP            NODE    &#x000A;pc-daemonset-9bck8   1/1     Running   0          37s   10.244.1.43   node1     &#x000A;pc-daemonset-k224w   1/1     Running   0          37s   10.244.2.74   node2      &#x000A;&#x000A;# 删除daemonset&#x000A;[root@k8s-master01 ~]# kubectl delete -f pc-daemonset.yaml&#x000A;daemonset.apps &quot;pc-daemonset&quot; deleted&#x000A;```&#x000A;&#x000A;#### 6.6 Job&#x000A;&#x000A;Job，主要用于负责**批量处理(一次要处理指定数量任务)**短暂的**一次性(每个任务仅运行一次就结束)**任务。Job特点如下：&#x000A;&#x000A;- 当Job创建的pod执行成功结束时，Job将记录成功结束的pod数量&#x000A;- 当成功结束的pod达到指定的数量时，Job将完成执行&#x000A;&#x000A;![img](Kubenetes.assets/image-20200618213054113.png)&#x000A;&#x000A;Job的资源清单文件：&#x000A;&#x000A;&#x000A;&#x000A;```yaml&#x000A;apiVersion: batch/v1 # 版本号&#x000A;kind: Job # 类型       &#x000A;metadata: # 元数据&#x000A;  name: # rs名称 &#x000A;  namespace: # 所属命名空间 &#x000A;  labels: #标签&#x000A;    controller: job&#x000A;spec: # 详情描述&#x000A;  completions: 1 # 指定job需要成功运行Pods的次数。默认值: 1&#x000A;  parallelism: 1 # 指定job在任一时刻应该并发运行Pods的数量。默认值: 1&#x000A;  activeDeadlineSeconds: 30 # 指定job可运行的时间期限，超过时间还未结束，系统将会尝试进行终止。&#x000A;  backoffLimit: 6 # 指定job失败后进行重试的次数。默认是6&#x000A;  manualSelector: true # 是否可以使用selector选择器选择pod，默认是false&#x000A;  selector: # 选择器，通过它指定该控制器管理哪些pod&#x000A;    matchLabels:      # Labels匹配规则&#x000A;      app: counter-pod&#x000A;    matchExpressions: # Expressions匹配规则&#x000A;      - {key: app, operator: In, values: [counter-pod]}&#x000A;  template: # 模板，当副本数量不足时，会根据下面的模板创建pod副本&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: counter-pod&#x000A;    spec:&#x000A;      restartPolicy: Never # 重启策略只能设置为Never或者OnFailure&#x000A;      containers:&#x000A;      - name: counter&#x000A;        image: busybox:1.30&#x000A;        command: [&quot;bin/sh&quot;,&quot;-c&quot;,&quot;for i in 9 8 7 6 5 4 3 2 1; do echo $i;sleep 2;done&quot;]&#x000A;```&#x000A;&#x000A;```markdown&#x000A;关于重启策略设置的说明：&#x000A;    如果指定为OnFailure，则job会在pod出现故障时重启容器，而不是创建pod，failed次数不变&#x000A;    如果指定为Never，则job会在pod出现故障时创建新的pod，并且故障pod不会消失，也不会重启，failed次数加1&#x000A;    如果指定为Always的话，就意味着一直重启，意味着job任务会重复去执行了，当然不对，所以不能设置为Always&#x000A;```&#x000A;&#x000A;创建pc-job.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: batch/v1&#x000A;kind: Job      &#x000A;metadata:&#x000A;  name: pc-job&#x000A;  namespace: dev&#x000A;spec:&#x000A;  manualSelector: true&#x000A;  selector:&#x000A;    matchLabels:&#x000A;      app: counter-pod&#x000A;  template:&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: counter-pod&#x000A;    spec:&#x000A;      restartPolicy: Never&#x000A;      containers:&#x000A;      - name: counter&#x000A;        image: busybox:1.30&#x000A;        command: [&quot;bin/sh&quot;,&quot;-c&quot;,&quot;for i in 9 8 7 6 5 4 3 2 1; do echo $i;sleep 3;done&quot;]&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建job&#x000A;[root@k8s-master01 ~]# kubectl create -f pc-job.yaml&#x000A;job.batch/pc-job created&#x000A;&#x000A;# 查看job&#x000A;[root@k8s-master01 ~]# kubectl get job -n dev -o wide  -w&#x000A;NAME     COMPLETIONS   DURATION   AGE   CONTAINERS   IMAGES         SELECTOR&#x000A;pc-job   0/1           21s        21s   counter      busybox:1.30   app=counter-pod&#x000A;pc-job   1/1           31s        79s   counter      busybox:1.30   app=counter-pod&#x000A;&#x000A;# 通过观察pod状态可以看到，pod在运行完毕任务后，就会变成Completed状态&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -w&#x000A;NAME           READY   STATUS     RESTARTS      AGE&#x000A;pc-job-rxg96   1/1     Running     0            29s&#x000A;pc-job-rxg96   0/1     Completed   0            33s&#x000A;&#x000A;# 接下来，调整下pod运行的总数量和并行数量 即：在spec下设置下面两个选项&#x000A;#  completions: 6 # 指定job需要成功运行Pods的次数为6&#x000A;#  parallelism: 3 # 指定job并发运行Pods的数量为3&#x000A;#  然后重新运行job，观察效果，此时会发现，job会每次运行3个pod，总共执行了6个pod&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -w&#x000A;NAME           READY   STATUS    RESTARTS   AGE&#x000A;pc-job-684ft   1/1     Running   0          5s&#x000A;pc-job-jhj49   1/1     Running   0          5s&#x000A;pc-job-pfcvh   1/1     Running   0          5s&#x000A;pc-job-684ft   0/1     Completed   0          11s&#x000A;pc-job-v7rhr   0/1     Pending     0          0s&#x000A;pc-job-v7rhr   0/1     Pending     0          0s&#x000A;pc-job-v7rhr   0/1     ContainerCreating   0          0s&#x000A;pc-job-jhj49   0/1     Completed           0          11s&#x000A;pc-job-fhwf7   0/1     Pending             0          0s&#x000A;pc-job-fhwf7   0/1     Pending             0          0s&#x000A;pc-job-pfcvh   0/1     Completed           0          11s&#x000A;pc-job-5vg2j   0/1     Pending             0          0s&#x000A;pc-job-fhwf7   0/1     ContainerCreating   0          0s&#x000A;pc-job-5vg2j   0/1     Pending             0          0s&#x000A;pc-job-5vg2j   0/1     ContainerCreating   0          0s&#x000A;pc-job-fhwf7   1/1     Running             0          2s&#x000A;pc-job-v7rhr   1/1     Running             0          2s&#x000A;pc-job-5vg2j   1/1     Running             0          3s&#x000A;pc-job-fhwf7   0/1     Completed           0          12s&#x000A;pc-job-v7rhr   0/1     Completed           0          12s&#x000A;pc-job-5vg2j   0/1     Completed           0          12s&#x000A;&#x000A;# 删除job&#x000A;[root@k8s-master01 ~]# kubectl delete -f pc-job.yaml&#x000A;job.batch &quot;pc-job&quot; deleted&#x000A;```&#x000A;&#x000A;#### 6.7 CronJob(CJ)&#x000A;&#x000A;CronJob控制器以 Job控制器资源为其管控对象，并借助它管理pod资源对象，Job控制器定义的作业任务在其控制器资源创建之后便会立即执行，但CronJob可以以类似于Linux操作系统的周期性任务作业计划的方式控制其运行**时间点**及**重复运行**的方式。也就是说，**CronJob可以在特定的时间点(反复的)去运行job任务**。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200618213149531.png)&#x000A;&#x000A;CronJob的资源清单文件：&#x000A;&#x000A;```yaml&#x000A;apiVersion: batch/v1beta1 # 版本号&#x000A;kind: CronJob # 类型       &#x000A;metadata: # 元数据&#x000A;  name: # rs名称 &#x000A;  namespace: # 所属命名空间 &#x000A;  labels: #标签&#x000A;    controller: cronjob&#x000A;spec: # 详情描述&#x000A;  schedule: # cron格式的作业调度运行时间点,用于控制任务在什么时间执行&#x000A;  concurrencyPolicy: # 并发执行策略，用于定义前一次作业运行尚未完成时是否以及如何运行后一次的作业&#x000A;  failedJobHistoryLimit: # 为失败的任务执行保留的历史记录数，默认为1&#x000A;  successfulJobHistoryLimit: # 为成功的任务执行保留的历史记录数，默认为3&#x000A;  startingDeadlineSeconds: # 启动作业错误的超时时长&#x000A;  jobTemplate: # job控制器模板，用于为cronjob控制器生成job对象;下面其实就是job的定义&#x000A;    metadata:&#x000A;    spec:&#x000A;      completions: 1&#x000A;      parallelism: 1&#x000A;      activeDeadlineSeconds: 30&#x000A;      backoffLimit: 6&#x000A;      manualSelector: true&#x000A;      selector:&#x000A;        matchLabels:&#x000A;          app: counter-pod&#x000A;        matchExpressions: 规则&#x000A;          - {key: app, operator: In, values: [counter-pod]}&#x000A;      template:&#x000A;        metadata:&#x000A;          labels:&#x000A;            app: counter-pod&#x000A;        spec:&#x000A;          restartPolicy: Never &#x000A;          containers:&#x000A;          - name: counter&#x000A;            image: busybox:1.30&#x000A;            command: [&quot;bin/sh&quot;,&quot;-c&quot;,&quot;for i in 9 8 7 6 5 4 3 2 1; do echo $i;sleep 20;done&quot;]&#x000A;```&#x000A;&#x000A;```markdown&#x000A;需要重点解释的几个选项：&#x000A;schedule: cron表达式，用于指定任务的执行时间&#x000A;    */1    *      *    *     *&#x000A;    &lt;分钟&gt; &lt;小时&gt; &lt;日&gt; &lt;月份&gt; &lt;星期&gt;&#x000A;&#x000A;    分钟 值从 0 到 59.&#x000A;    小时 值从 0 到 23.&#x000A;    日 值从 1 到 31.&#x000A;    月 值从 1 到 12.&#x000A;    星期 值从 0 到 6, 0 代表星期日&#x000A;    多个时间可以用逗号隔开； 范围可以用连字符给出；*可以作为通配符； /表示每...&#x000A;concurrencyPolicy:&#x000A;    Allow:   允许Jobs并发运行(默认)&#x000A;    Forbid:  禁止并发运行，如果上一次运行尚未完成，则跳过下一次运行&#x000A;    Replace: 替换，取消当前正在运行的作业并用新作业替换它&#x000A;```&#x000A;&#x000A;创建pc-cronjob.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: batch/v1beta1&#x000A;kind: CronJob&#x000A;metadata:&#x000A;  name: pc-cronjob&#x000A;  namespace: dev&#x000A;  labels:&#x000A;    controller: cronjob&#x000A;spec:&#x000A;  schedule: &quot;*/1 * * * *&quot;&#x000A;  jobTemplate:&#x000A;    metadata:&#x000A;    spec:&#x000A;      template:&#x000A;        spec:&#x000A;          restartPolicy: Never&#x000A;          containers:&#x000A;          - name: counter&#x000A;            image: busybox:1.30&#x000A;            command: [&quot;bin/sh&quot;,&quot;-c&quot;,&quot;for i in 9 8 7 6 5 4 3 2 1; do echo $i;sleep 3;done&quot;]&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建cronjob&#x000A;[root@k8s-master01 ~]# kubectl create -f pc-cronjob.yaml&#x000A;cronjob.batch/pc-cronjob created&#x000A;&#x000A;# 查看cronjob&#x000A;[root@k8s-master01 ~]# kubectl get cronjobs -n dev&#x000A;NAME         SCHEDULE      SUSPEND   ACTIVE   LAST SCHEDULE   AGE&#x000A;pc-cronjob   */1 * * * *   False     0        &lt;none&gt;          6s&#x000A;&#x000A;# 查看job&#x000A;[root@k8s-master01 ~]# kubectl get jobs -n dev&#x000A;NAME                    COMPLETIONS   DURATION   AGE&#x000A;pc-cronjob-1592587800   1/1           28s        3m26s&#x000A;pc-cronjob-1592587860   1/1           28s        2m26s&#x000A;pc-cronjob-1592587920   1/1           28s        86s&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev&#x000A;pc-cronjob-1592587800-x4tsm   0/1     Completed   0          2m24s&#x000A;pc-cronjob-1592587860-r5gv4   0/1     Completed   0          84s&#x000A;pc-cronjob-1592587920-9dxxq   1/1     Running     0          24s&#x000A;&#x000A;&#x000A;# 删除cronjob&#x000A;[root@k8s-master01 ~]# kubectl  delete -f pc-cronjob.yaml&#x000A;cronjob.batch &quot;pc-cronjob&quot; deleted&#x000A;```&#x000A;&#x000A; &#x000A;&#x000A;### 7. Service详解&#x000A;&#x000A;#### 7.1 Service介绍&#x000A;&#x000A;在kubernetes中，pod是应用程序的载体，我们可以通过pod的ip来访问应用程序，但是pod的ip地址不是固定的，这也就意味着不方便直接采用pod的ip对服务进行访问。&#x000A;&#x000A;为了解决这个问题，kubernetes提供了Service资源，Service会对提供同一个服务的多个pod进行聚合，并且提供一个统一的入口地址。通过访问Service的入口地址就能访问到后面的pod服务。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200408194716912-1626783758946.png)&#x000A;&#x000A;Service在很多情况下只是一个概念，真正起作用的其实是kube-proxy服务进程，每个Node节点上都运行着一个kube-proxy服务进程。当创建Service的时候会通过api-server向etcd写入创建的service的信息，而kube-proxy会基于监听的机制发现这种Service的变动，然后**它会将最新的Service信息转换成对应的访问规则**。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200509121254425.png)&#x000A;&#x000A;&#x000A;&#x000A;```&#x000A;# 10.97.97.97:80 是service提供的访问入口&#x000A;# 当访问这个入口的时候，可以发现后面有三个pod的服务在等待调用，&#x000A;# kube-proxy会基于rr（轮询）的策略，将请求分发到其中一个pod上去&#x000A;# 这个规则会同时在集群内的所有节点上都生成，所以在任何一个节点上，都可以访问。&#x000A;[root@node1 ~]# ipvsadm -Ln&#x000A;IP Virtual Server version 1.2.1 (size=4096)&#x000A;Prot LocalAddress:Port Scheduler Flags&#x000A;  -&gt; RemoteAddress:Port           Forward Weight ActiveConn InActConn&#x000A;TCP  10.97.97.97:80 rr&#x000A;  -&gt; 10.244.1.39:80               Masq    1      0          0&#x000A;  -&gt; 10.244.1.40:80               Masq    1      0          0&#x000A;  -&gt; 10.244.2.33:80               Masq    1      0          0&#x000A;```&#x000A;&#x000A;kube-proxy目前支持三种工作模式:&#x000A;&#x000A;##### 7.1.1 userspace 模式&#x000A;&#x000A;userspace模式下，kube-proxy会为每一个Service创建一个监听端口，发向Cluster IP的请求被Iptables规则重定向到kube-proxy监听的端口上，kube-proxy根据LB算法选择一个提供服务的Pod并和其建立链接，以将请求转发到Pod上。  该模式下，kube-proxy充当了一个四层负责均衡器的角色。由于kube-proxy运行在userspace中，在进行转发处理时会增加内核和用户空间之间的数据拷贝，虽然比较稳定，但是效率比较低。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200509151424280.png)&#x000A;&#x000A;##### 7.1.2 iptables 模式&#x000A;&#x000A;iptables模式下，kube-proxy为service后端的每个Pod创建对应的iptables规则，直接将发向Cluster IP的请求重定向到一个Pod IP。  该模式下kube-proxy不承担四层负责均衡器的角色，只负责创建iptables规则。该模式的优点是较userspace模式效率更高，但不能提供灵活的LB策略，当后端Pod不可用时也无法进行重试。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200509152947714.png)&#x000A;&#x000A;##### 7.1.3 ipvs 模式&#x000A;&#x000A;ipvs模式和iptables类似，kube-proxy监控Pod的变化并创建相应的ipvs规则。ipvs相对iptables转发效率更高。除此以外，ipvs支持更多的LB算法。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200509153731363.png)&#x000A;&#x000A;```shell&#x000A;# 此模式必须安装ipvs内核模块，否则会降级为iptables&#x000A;# 开启ipvs&#x000A;[root@k8s-master01 ~]# kubectl edit cm kube-proxy -n kube-system&#x000A;# 修改mode: &quot;ipvs&quot;&#x000A;[root@k8s-master01 ~]# kubectl delete pod -l k8s-app=kube-proxy -n kube-system&#x000A;[root@node1 ~]# ipvsadm -Ln&#x000A;IP Virtual Server version 1.2.1 (size=4096)&#x000A;Prot LocalAddress:Port Scheduler Flags&#x000A;  -&gt; RemoteAddress:Port           Forward Weight ActiveConn InActConn&#x000A;TCP  10.97.97.97:80 rr&#x000A;  -&gt; 10.244.1.39:80               Masq    1      0          0&#x000A;  -&gt; 10.244.1.40:80               Masq    1      0          0&#x000A;  -&gt; 10.244.2.33:80               Masq    1      0          0&#x000A;```&#x000A;&#x000A;#### 7.2 Service类型&#x000A;&#x000A;Service的资源清单文件：&#x000A;&#x000A;```yaml&#x000A;kind: Service  # 资源类型&#x000A;apiVersion: v1  # 资源版本&#x000A;metadata: # 元数据&#x000A;  name: service # 资源名称&#x000A;  namespace: dev # 命名空间&#x000A;spec: # 描述&#x000A;  selector: # 标签选择器，用于确定当前service代理哪些pod&#x000A;    app: nginx&#x000A;  type: # Service类型，指定service的访问方式&#x000A;  clusterIP:  # 虚拟服务的ip地址&#x000A;  sessionAffinity: # session亲和性，支持ClientIP、None两个选项&#x000A;  ports: # 端口信息&#x000A;    - protocol: TCP &#x000A;      port: 3017  # service端口&#x000A;      targetPort: 5003 # pod端口&#x000A;      nodePort: 31122 # 主机端口&#x000A;```&#x000A;&#x000A;- ClusterIP：默认值，它是Kubernetes系统自动分配的虚拟IP，只能在集群内部访问&#x000A;- NodePort：将Service通过指定的Node上的端口暴露给外部，通过此方法，就可以在集群外部访问服务&#x000A;- LoadBalancer：使用外接负载均衡器完成到服务的负载分发，注意此模式需要外部云环境支持&#x000A;- ExternalName： 把集群外部的服务引入集群内部，直接使用&#x000A;&#x000A;#### 7.3 Service使用&#x000A;&#x000A;##### 7.3.1 实验环境准备&#x000A;&#x000A;在使用service之前，首先利用Deployment创建出3个pod，注意要为pod设置`app=nginx-pod`的标签&#x000A;&#x000A;创建deployment.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1&#x000A;kind: Deployment      &#x000A;metadata:&#x000A;  name: pc-deployment&#x000A;  namespace: dev&#x000A;spec: &#x000A;  replicas: 3&#x000A;  selector:&#x000A;    matchLabels:&#x000A;      app: nginx-pod&#x000A;  template:&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: nginx-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: nginx&#x000A;        image: nginx:1.17.1&#x000A;        ports:&#x000A;        - containerPort: 80&#x000A;```&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# kubectl create -f deployment.yaml&#x000A;deployment.apps/pc-deployment created&#x000A;&#x000A;# 查看pod详情&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -o wide --show-labels&#x000A;NAME                             READY   STATUS     IP            NODE     LABELS&#x000A;pc-deployment-66cb59b984-8p84h   1/1     Running    10.244.1.39   node1    app=nginx-pod&#x000A;pc-deployment-66cb59b984-vx8vx   1/1     Running    10.244.2.33   node2    app=nginx-pod&#x000A;pc-deployment-66cb59b984-wnncx   1/1     Running    10.244.1.40   node1    app=nginx-pod&#x000A;&#x000A;# 为了方便后面的测试，修改下三台nginx的index.html页面（三台修改的IP地址不一致）&#x000A;# kubectl exec -it pc-deployment-66cb59b984-8p84h -n dev /bin/sh&#x000A;# echo &quot;10.244.1.39&quot; &gt; /usr/share/nginx/html/index.html&#x000A;&#x000A;#修改完毕之后，访问测试&#x000A;[root@k8s-master01 ~]# curl 10.244.1.39&#x000A;10.244.1.39&#x000A;[root@k8s-master01 ~]# curl 10.244.2.33&#x000A;10.244.2.33&#x000A;[root@k8s-master01 ~]# curl 10.244.1.40&#x000A;10.244.1.40&#x000A;```&#x000A;&#x000A;##### 7.3.2 ClusterIP类型的Service&#x000A;&#x000A;创建service-clusterip.yaml文件&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Service&#x000A;metadata:&#x000A;  name: service-clusterip&#x000A;  namespace: dev&#x000A;spec:&#x000A;  selector:&#x000A;    app: nginx-pod&#x000A;  clusterIP: 10.97.97.97 # service的ip地址，如果不写，默认会生成一个&#x000A;  type: ClusterIP&#x000A;  ports:&#x000A;  - port: 80  # Service端口       &#x000A;    targetPort: 80 # pod端口&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建service&#x000A;[root@k8s-master01 ~]# kubectl create -f service-clusterip.yaml&#x000A;service/service-clusterip created&#x000A;&#x000A;# 查看service&#x000A;[root@k8s-master01 ~]# kubectl get svc -n dev -o wide&#x000A;NAME                TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)   AGE   SELECTOR&#x000A;service-clusterip   ClusterIP   10.97.97.97   &lt;none&gt;        80/TCP    13s   app=nginx-pod&#x000A;&#x000A;# 查看service的详细信息&#x000A;# 在这里有一个Endpoints列表，里面就是当前service可以负载到的服务入口&#x000A;[root@k8s-master01 ~]# kubectl describe svc service-clusterip -n dev&#x000A;Name:              service-clusterip&#x000A;Namespace:         dev&#x000A;Labels:            &lt;none&gt;&#x000A;Annotations:       &lt;none&gt;&#x000A;Selector:          app=nginx-pod&#x000A;Type:              ClusterIP&#x000A;IP:                10.97.97.97&#x000A;Port:              &lt;unset&gt;  80/TCP&#x000A;TargetPort:        80/TCP&#x000A;Endpoints:         10.244.1.39:80,10.244.1.40:80,10.244.2.33:80&#x000A;Session Affinity:  None&#x000A;Events:            &lt;none&gt;&#x000A;&#x000A;# 查看ipvs的映射规则&#x000A;[root@k8s-master01 ~]# ipvsadm -Ln&#x000A;TCP  10.97.97.97:80 rr&#x000A;  -&gt; 10.244.1.39:80               Masq    1      0          0&#x000A;  -&gt; 10.244.1.40:80               Masq    1      0          0&#x000A;  -&gt; 10.244.2.33:80               Masq    1      0          0&#x000A;&#x000A;# 访问10.97.97.97:80观察效果&#x000A;[root@k8s-master01 ~]# curl 10.97.97.97:80&#x000A;10.244.2.33&#x000A;```&#x000A;&#x000A;##### 7.3.3 Endpoint&#x000A;&#x000A;Endpoint是kubernetes中的一个资源对象，存储在etcd中，用来记录一个service对应的所有pod的访问地址，它是根据service配置文件中selector描述产生的。&#x000A;&#x000A;一个Service由一组Pod组成，这些Pod通过Endpoints暴露出来，**Endpoints是实现实际服务的端点集合**。换句话说，service和pod之间的联系是通过endpoints实现的。&#x000A;&#x000A;![image-20200509191917069](Kubenetes.assets/image-20200509191917069.png)&#x000A;&#x000A;**负载分发策略**&#x000A;&#x000A;对Service的访问被分发到了后端的Pod上去，目前kubernetes提供了两种负载分发策略：&#x000A;&#x000A;- 如果不定义，默认使用kube-proxy的策略，比如随机、轮询&#x000A;&#x000A;- 基于客户端地址的会话保持模式，即来自同一个客户端发起的所有请求都会转发到固定的一个Pod上&#x000A;&#x000A;  此模式可以使在spec中添加`sessionAffinity:ClientIP`选项&#x000A;&#x000A;```shell&#x000A;# 查看ipvs的映射规则【rr 轮询】&#x000A;[root@k8s-master01 ~]# ipvsadm -Ln&#x000A;TCP  10.97.97.97:80 rr&#x000A;  -&gt; 10.244.1.39:80               Masq    1      0          0&#x000A;  -&gt; 10.244.1.40:80               Masq    1      0          0&#x000A;  -&gt; 10.244.2.33:80               Masq    1      0          0&#x000A;&#x000A;# 循环访问测试&#x000A;[root@k8s-master01 ~]# while true;do curl 10.97.97.97:80; sleep 5; done;&#x000A;10.244.1.40&#x000A;10.244.1.39&#x000A;10.244.2.33&#x000A;10.244.1.40&#x000A;10.244.1.39&#x000A;10.244.2.33&#x000A;&#x000A;# 修改分发策略----sessionAffinity:ClientIP&#x000A;&#x000A;# 查看ipvs规则【persistent 代表持久】&#x000A;[root@k8s-master01 ~]# ipvsadm -Ln&#x000A;TCP  10.97.97.97:80 rr persistent 10800&#x000A;  -&gt; 10.244.1.39:80               Masq    1      0          0&#x000A;  -&gt; 10.244.1.40:80               Masq    1      0          0&#x000A;  -&gt; 10.244.2.33:80               Masq    1      0          0&#x000A;&#x000A;# 循环访问测试&#x000A;[root@k8s-master01 ~]# while true;do curl 10.97.97.97; sleep 5; done;&#x000A;10.244.2.33&#x000A;10.244.2.33&#x000A;10.244.2.33&#x000A;  &#x000A;# 删除service&#x000A;[root@k8s-master01 ~]# kubectl delete -f service-clusterip.yaml&#x000A;service &quot;service-clusterip&quot; deleted&#x000A;```&#x000A;&#x000A;##### 7.3.4 HeadLiness类型的Service&#x000A;&#x000A;在某些场景中，开发人员可能不想使用Service提供的负载均衡功能，而希望自己来控制负载均衡策略，针对这种情况，kubernetes提供了HeadLiness Service，这类Service不会分配Cluster IP，如果想要访问service，只能通过service的域名进行查询。&#x000A;&#x000A;创建service-headliness.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Service&#x000A;metadata:&#x000A;  name: service-headliness&#x000A;  namespace: dev&#x000A;spec:&#x000A;  selector:&#x000A;    app: nginx-pod&#x000A;  clusterIP: None # 将clusterIP设置为None，即可创建headliness Service&#x000A;  type: ClusterIP&#x000A;  ports:&#x000A;  - port: 80    &#x000A;    targetPort: 80&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建service&#x000A;[root@k8s-master01 ~]# kubectl create -f service-headliness.yaml&#x000A;service/service-headliness created&#x000A;&#x000A;# 获取service， 发现CLUSTER-IP未分配&#x000A;[root@k8s-master01 ~]# kubectl get svc service-headliness -n dev -o wide&#x000A;NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE   SELECTOR&#x000A;service-headliness   ClusterIP   None         &lt;none&gt;        80/TCP    11s   app=nginx-pod&#x000A;&#x000A;# 查看service详情&#x000A;[root@k8s-master01 ~]# kubectl describe svc service-headliness  -n dev&#x000A;Name:              service-headliness&#x000A;Namespace:         dev&#x000A;Labels:            &lt;none&gt;&#x000A;Annotations:       &lt;none&gt;&#x000A;Selector:          app=nginx-pod&#x000A;Type:              ClusterIP&#x000A;IP:                None&#x000A;Port:              &lt;unset&gt;  80/TCP&#x000A;TargetPort:        80/TCP&#x000A;Endpoints:         10.244.1.39:80,10.244.1.40:80,10.244.2.33:80&#x000A;Session Affinity:  None&#x000A;Events:            &lt;none&gt;&#x000A;&#x000A;# 查看域名的解析情况&#x000A;[root@k8s-master01 ~]# kubectl exec -it pc-deployment-66cb59b984-8p84h -n dev /bin/sh&#x000A;/ # cat /etc/resolv.conf&#x000A;nameserver 10.96.0.10&#x000A;search dev.svc.cluster.local svc.cluster.local cluster.local&#x000A;&#x000A;[root@k8s-master01 ~]# dig @10.96.0.10 service-headliness.dev.svc.cluster.local&#x000A;service-headliness.dev.svc.cluster.local. 30 IN A 10.244.1.40&#x000A;service-headliness.dev.svc.cluster.local. 30 IN A 10.244.1.39&#x000A;service-headliness.dev.svc.cluster.local. 30 IN A 10.244.2.33&#x000A;```&#x000A;&#x000A;##### 7.3.5 NodePort类型的Service&#x000A;&#x000A;在之前的样例中，创建的Service的ip地址只有集群内部才可以访问，如果希望将Service暴露给集群外部使用，那么就要使用到另外一种类型的Service，称为NodePort类型。NodePort的工作原理其实就是**将service的端口映射到Node的一个端口上**，然后就可以通过`NodeIp:NodePort`来访问service了。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200620175731338.png)&#x000A;&#x000A;创建service-nodeport.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Service&#x000A;metadata:&#x000A;  name: service-nodeport&#x000A;  namespace: dev&#x000A;spec:&#x000A;  selector:&#x000A;    app: nginx-pod&#x000A;  type: NodePort # service类型&#x000A;  ports:&#x000A;  - port: 80&#x000A;    nodePort: 30002 # 指定绑定的node的端口(默认的取值范围是：30000-32767), 如果不指定，会默认分配&#x000A;    targetPort: 80&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建service&#x000A;[root@k8s-master01 ~]# kubectl create -f service-nodeport.yaml&#x000A;service/service-nodeport created&#x000A;&#x000A;# 查看service&#x000A;[root@k8s-master01 ~]# kubectl get svc -n dev -o wide&#x000A;NAME               TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)       SELECTOR&#x000A;service-nodeport   NodePort   10.105.64.191   &lt;none&gt;        80:30002/TCP  app=nginx-pod&#x000A;&#x000A;# 接下来可以通过电脑主机的浏览器去访问集群中任意一个nodeip的30002端口，即可访问到pod&#x000A;```&#x000A;&#x000A;##### 7.3.6 LoadBalancer类型的Service&#x000A;&#x000A;LoadBalancer和NodePort很相似，目的都是向外部暴露一个端口，区别在于LoadBalancer会在集群的外部再来做一个负载均衡设备，而这个设备需要外部环境支持的，外部服务发送到这个设备上的请求，会被设备负载之后转发到集群中。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200510103945494.png)&#x000A;&#x000A;##### 7.3.7 ExternalName类型的Service&#x000A;&#x000A;ExternalName类型的Service用于引入集群外部的服务，它通过`externalName`属性指定外部一个服务的地址，然后在集群内部访问此service就可以访问到外部的服务了。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200510113311209.png)&#x000A;&#x000A;```shell&#x000A;apiVersion: v1&#x000A;kind: Service&#x000A;metadata:&#x000A;  name: service-externalname&#x000A;  namespace: dev&#x000A;spec:&#x000A;  type: ExternalName # service类型&#x000A;  externalName: www.baidu.com  #改成ip地址也可以&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建service&#x000A;[root@k8s-master01 ~]# kubectl  create -f service-externalname.yaml&#x000A;service/service-externalname created&#x000A;&#x000A;# 域名解析&#x000A;[root@k8s-master01 ~]# dig @10.96.0.10 service-externalname.dev.svc.cluster.local&#x000A;service-externalname.dev.svc.cluster.local. 30 IN CNAME www.baidu.com.&#x000A;www.baidu.com.          30      IN      CNAME   www.a.shifen.com.&#x000A;www.a.shifen.com.       30      IN      A       39.156.66.18&#x000A;www.a.shifen.com.       30      IN      A       39.156.66.14&#x000A;```&#x000A;&#x000A;#### 7.4 Ingress介绍&#x000A;&#x000A;在前面课程中已经提到，Service对集群之外暴露服务的主要方式有两种：NotePort和LoadBalancer，但是这两种方式，都有一定的缺点：&#x000A;&#x000A;- NodePort方式的缺点是会占用很多集群机器的端口，那么当集群服务变多的时候，这个缺点就愈发明显&#x000A;- LB方式的缺点是每个service需要一个LB，浪费、麻烦，并且需要kubernetes之外设备的支持&#x000A;&#x000A;基于这种现状，kubernetes提供了Ingress资源对象，Ingress只需要一个NodePort或者一个LB就可以满足暴露多个Service的需求。工作机制大致如下图表示：&#x000A;&#x000A;![img](Kubenetes.assets/image-20200623092808049.png)&#x000A;&#x000A;实际上，Ingress相当于一个7层的负载均衡器，是kubernetes对反向代理的一个抽象，它的工作原理类似于Nginx，可以理解成在**Ingress里建立诸多映射规则，Ingress Controller通过监听这些配置规则并转化成Nginx的反向代理配置 , 然后对外部提供服务**。在这里有两个核心概念：&#x000A;&#x000A;- ingress：kubernetes中的一个对象，作用是定义请求如何转发到service的规则&#x000A;- ingress controller：具体实现反向代理及负载均衡的程序，对ingress定义的规则进行解析，根据配置的规则来实现请求转发，实现方式有很多，比如Nginx, Contour, Haproxy等等&#x000A;&#x000A;Ingress（以Nginx为例）的工作原理如下：&#x000A;&#x000A;1. 用户编写Ingress规则，说明哪个域名对应kubernetes集群中的哪个Service&#x000A;2. Ingress控制器动态感知Ingress服务规则的变化，然后生成一段对应的Nginx反向代理配置&#x000A;3. Ingress控制器会将生成的Nginx配置写入到一个运行着的Nginx服务中，并动态更新&#x000A;4. 到此为止，其实真正在工作的就是一个Nginx了，内部配置了用户定义的请求转发规则&#x000A;&#x000A;![img](Kubenetes.assets/image-20200516112704764.png)&#x000A;&#x000A;#### 7.5 Ingress使用&#x000A;&#x000A;##### 7.5.1 环境准备 搭建ingress环境&#x000A;&#x000A;```makefile&#x000A;# 创建文件夹&#x000A;[root@k8s-master01 ~]# mkdir ingress-controller&#x000A;[root@k8s-master01 ~]# cd ingress-controller/&#x000A;&#x000A;# 获取ingress-nginx，本次案例使用的是0.30版本&#x000A;[root@k8s-master01 ingress-controller]# wget https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.30.0/deploy/static/mandatory.yaml&#x000A;[root@k8s-master01 ingress-controller]# wget https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.30.0/deploy/static/provider/baremetal/service-nodeport.yaml&#x000A;&#x000A;# 修改mandatory.yaml文件中的仓库&#x000A;# 修改quay.io/kubernetes-ingress-controller/nginx-ingress-controller:0.30.0&#x000A;# 为quay-mirror.qiniu.com/kubernetes-ingress-controller/nginx-ingress-controller:0.30.0&#x000A;# 创建ingress-nginx&#x000A;[root@k8s-master01 ingress-controller]# kubectl apply -f ./&#x000A;&#x000A;# 查看ingress-nginx&#x000A;[root@k8s-master01 ingress-controller]# kubectl get pod -n ingress-nginx&#x000A;NAME                                           READY   STATUS    RESTARTS   AGE&#x000A;pod/nginx-ingress-controller-fbf967dd5-4qpbp   1/1     Running   0          12h&#x000A;&#x000A;# 查看service&#x000A;[root@k8s-master01 ingress-controller]# kubectl get svc -n ingress-nginx&#x000A;NAME            TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)                      AGE&#x000A;ingress-nginx   NodePort   10.98.75.163   &lt;none&gt;        80:32240/TCP,443:31335/TCP   11h&#x000A;```&#x000A;&#x000A;##### 7.5.2 准备service和pod&#x000A;&#x000A;为了后面的实验比较方便，创建如下图所示的模型&#x000A;&#x000A;![img](Kubenetes.assets/image-20200516102419998.png)&#x000A;&#x000A;创建tomcat-nginx.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1&#x000A;kind: Deployment&#x000A;metadata:&#x000A;  name: nginx-deployment&#x000A;  namespace: dev&#x000A;spec:&#x000A;  replicas: 3&#x000A;  selector:&#x000A;    matchLabels:&#x000A;      app: nginx-pod&#x000A;  template:&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: nginx-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: nginx&#x000A;        image: nginx:1.17.1&#x000A;        ports:&#x000A;        - containerPort: 80&#x000A;&#x000A;---&#x000A;&#x000A;apiVersion: apps/v1&#x000A;kind: Deployment&#x000A;metadata:&#x000A;  name: tomcat-deployment&#x000A;  namespace: dev&#x000A;spec:&#x000A;  replicas: 3&#x000A;  selector:&#x000A;    matchLabels:&#x000A;      app: tomcat-pod&#x000A;  template:&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: tomcat-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: tomcat&#x000A;        image: tomcat:8.5-jre10-slim&#x000A;        ports:&#x000A;        - containerPort: 8080&#x000A;&#x000A;---&#x000A;&#x000A;apiVersion: v1&#x000A;kind: Service&#x000A;metadata:&#x000A;  name: nginx-service&#x000A;  namespace: dev&#x000A;spec:&#x000A;  selector:&#x000A;    app: nginx-pod&#x000A;  clusterIP: None&#x000A;  type: ClusterIP&#x000A;  ports:&#x000A;  - port: 80&#x000A;    targetPort: 80&#x000A;&#x000A;---&#x000A;&#x000A;apiVersion: v1&#x000A;kind: Service&#x000A;metadata:&#x000A;  name: tomcat-service&#x000A;  namespace: dev&#x000A;spec:&#x000A;  selector:&#x000A;    app: tomcat-pod&#x000A;  clusterIP: None&#x000A;  type: ClusterIP&#x000A;  ports:&#x000A;  - port: 8080&#x000A;    targetPort: 8080&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建&#x000A;[root@k8s-master01 ~]# kubectl create -f tomcat-nginx.yaml&#x000A;&#x000A;# 查看&#x000A;[root@k8s-master01 ~]# kubectl get svc -n dev&#x000A;NAME             TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)    AGE&#x000A;nginx-service    ClusterIP   None         &lt;none&gt;        80/TCP     48s&#x000A;tomcat-service   ClusterIP   None         &lt;none&gt;        8080/TCP   48s&#x000A;```&#x000A;&#x000A;##### 7.5.3 Http代理&#x000A;&#x000A;创建ingress-http.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: extensions/v1beta1&#x000A;kind: Ingress&#x000A;metadata:&#x000A;  name: ingress-http&#x000A;  namespace: dev&#x000A;spec:&#x000A;  rules:&#x000A;  - host: nginx.itheima.com&#x000A;    http:&#x000A;      paths:&#x000A;      - path: /&#x000A;        backend:&#x000A;          serviceName: nginx-service&#x000A;          servicePort: 80&#x000A;  - host: tomcat.itheima.com&#x000A;    http:&#x000A;      paths:&#x000A;      - path: /&#x000A;        backend:&#x000A;          serviceName: tomcat-service&#x000A;          servicePort: 8080&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建&#x000A;[root@k8s-master01 ~]# kubectl create -f ingress-http.yaml&#x000A;ingress.extensions/ingress-http created&#x000A;&#x000A;# 查看&#x000A;[root@k8s-master01 ~]# kubectl get ing ingress-http -n dev&#x000A;NAME           HOSTS                                  ADDRESS   PORTS   AGE&#x000A;ingress-http   nginx.itheima.com,tomcat.itheima.com             80      22s&#x000A;&#x000A;# 查看详情&#x000A;[root@k8s-master01 ~]# kubectl describe ing ingress-http  -n dev&#x000A;...&#x000A;Rules:&#x000A;Host                Path  Backends&#x000A;----                ----  --------&#x000A;nginx.itheima.com   / nginx-service:80 (10.244.1.96:80,10.244.1.97:80,10.244.2.112:80)&#x000A;tomcat.itheima.com  / tomcat-service:8080(10.244.1.94:8080,10.244.1.95:8080,10.244.2.111:8080)&#x000A;...&#x000A;&#x000A;# 接下来,在本地电脑上配置host文件,解析上面的两个域名到192.168.109.100(master)上&#x000A;# 然后,就可以分别访问tomcat.itheima.com:32240  和  nginx.itheima.com:32240 查看效果了&#x000A;```&#x000A;&#x000A;##### 7.5.4 Https代理&#x000A;&#x000A;创建证书&#x000A;&#x000A;```shell&#x000A;# 生成证书&#x000A;openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout tls.key -out tls.crt -subj &quot;/C=CN/ST=BJ/L=BJ/O=nginx/CN=itheima.com&quot;&#x000A;&#x000A;# 创建密钥&#x000A;kubectl create secret tls tls-secret --key tls.key --cert tls.crt&#x000A;```&#x000A;&#x000A;创建ingress-https.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: extensions/v1beta1&#x000A;kind: Ingress&#x000A;metadata:&#x000A;  name: ingress-https&#x000A;  namespace: dev&#x000A;spec:&#x000A;  tls:&#x000A;    - hosts:&#x000A;      - nginx.itheima.com&#x000A;      - tomcat.itheima.com&#x000A;      secretName: tls-secret # 指定秘钥&#x000A;  rules:&#x000A;  - host: nginx.itheima.com&#x000A;    http:&#x000A;      paths:&#x000A;      - path: /&#x000A;        backend:&#x000A;          serviceName: nginx-service&#x000A;          servicePort: 80&#x000A;  - host: tomcat.itheima.com&#x000A;    http:&#x000A;      paths:&#x000A;      - path: /&#x000A;        backend:&#x000A;          serviceName: tomcat-service&#x000A;          servicePort: 8080&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建&#x000A;[root@k8s-master01 ~]# kubectl create -f ingress-https.yaml&#x000A;ingress.extensions/ingress-https created&#x000A;&#x000A;# 查看&#x000A;[root@k8s-master01 ~]# kubectl get ing ingress-https -n dev&#x000A;NAME            HOSTS                                  ADDRESS         PORTS     AGE&#x000A;ingress-https   nginx.itheima.com,tomcat.itheima.com   10.104.184.38   80, 443   2m42s&#x000A;&#x000A;# 查看详情&#x000A;[root@k8s-master01 ~]# kubectl describe ing ingress-https -n dev&#x000A;...&#x000A;TLS:&#x000A;  tls-secret terminates nginx.itheima.com,tomcat.itheima.com&#x000A;Rules:&#x000A;Host              Path Backends&#x000A;----              ---- --------&#x000A;nginx.itheima.com  /  nginx-service:80 (10.244.1.97:80,10.244.1.98:80,10.244.2.119:80)&#x000A;tomcat.itheima.com /  tomcat-service:8080(10.244.1.99:8080,10.244.2.117:8080,10.244.2.120:8080)&#x000A;...&#x000A;&#x000A;# 下面可以通过浏览器访问https://nginx.itheima.com:31335 和 https://tomcat.itheima.com:31335来查看了&#x000A;```&#x000A;&#x000A;### 8. 数据存储&#x000A;&#x000A;在前面已经提到，容器的生命周期可能很短，会被频繁地创建和销毁。那么容器在销毁时，保存在容器中的数据也会被清除。这种结果对用户来说，在某些情况下是不乐意看到的。为了持久化保存容器的数据，kubernetes引入了Volume的概念。&#x000A;&#x000A;Volume是Pod中能够被多个容器访问的共享目录，它被定义在Pod上，然后被一个Pod里的多个容器挂载到具体的文件目录下，kubernetes通过Volume实现同一个Pod中不同容器之间的数据共享以及数据的持久化存储。Volume的生命容器不与Pod中单个容器的生命周期相关，当容器终止或者重启时，Volume中的数据也不会丢失。&#x000A;&#x000A;kubernetes的Volume支持多种类型，比较常见的有下面几个：&#x000A;&#x000A;- 简单存储：EmptyDir、HostPath、NFS&#x000A;- 高级存储：PV、PVC&#x000A;- 配置存储：ConfigMap、Secret&#x000A;&#x000A;#### 8.1 基本存储&#x000A;&#x000A;##### 8.1.1 EmptyDir&#x000A;&#x000A;EmptyDir是最基础的Volume类型，一个EmptyDir就是Host上的一个空目录。&#x000A;&#x000A;EmptyDir是在Pod被分配到Node时创建的，它的初始内容为空，并且无须指定宿主机上对应的目录文件，因为kubernetes会自动分配一个目录，当Pod销毁时， EmptyDir中的数据也会被永久删除。 EmptyDir用途如下：&#x000A;&#x000A;- 临时空间，例如用于某些应用程序运行时所需的临时目录，且无须永久保留&#x000A;- 一个容器需要从另一个容器中获取数据的目录（多容器共享目录）&#x000A;&#x000A;接下来，通过一个容器之间文件共享的案例来使用一下EmptyDir。&#x000A;&#x000A;在一个Pod中准备两个容器nginx和busybox，然后声明一个Volume分别挂在到两个容器的目录中，然后nginx容器负责向Volume中写日志，busybox中通过命令将日志内容读到控制台。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200413174713773.png)&#x000A;&#x000A;创建一个volume-emptydir.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: volume-emptydir&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    ports:&#x000A;    - containerPort: 80&#x000A;    volumeMounts:  # 将logs-volume挂在到nginx容器中，对应的目录为 /var/log/nginx&#x000A;    - name: logs-volume&#x000A;      mountPath: /var/log/nginx&#x000A;  - name: busybox&#x000A;    image: busybox:1.30&#x000A;    command: [&quot;/bin/sh&quot;,&quot;-c&quot;,&quot;tail -f /logs/access.log&quot;] # 初始命令，动态读取指定文件中内容&#x000A;    volumeMounts:  # 将logs-volume 挂在到busybox容器中，对应的目录为 /logs&#x000A;    - name: logs-volume&#x000A;      mountPath: /logs&#x000A;  volumes: # 声明volume， name为logs-volume，类型为emptyDir&#x000A;  - name: logs-volume&#x000A;    emptyDir: {}&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f volume-emptydir.yaml&#x000A;pod/volume-emptydir created&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pods volume-emptydir -n dev -o wide&#x000A;NAME                  READY   STATUS    RESTARTS   AGE      IP       NODE   ...... &#x000A;volume-emptydir       2/2     Running   0          97s   10.42.2.9   node1  ......&#x000A;&#x000A;# 通过podIp访问nginx&#x000A;[root@k8s-master01 ~]# curl 10.42.2.9&#x000A;......&#x000A;&#x000A;# 通过kubectl logs命令查看指定容器的标准输出&#x000A;[root@k8s-master01 ~]# kubectl logs -f volume-emptydir -n dev -c busybox&#x000A;10.42.1.0 - - [27/Jun/2021:15:08:54 +0000] &quot;GET / HTTP/1.1&quot; 200 612 &quot;-&quot; &quot;curl/7.29.0&quot; &quot;-&quot;&#x000A;```&#x000A;&#x000A;##### 8.1.2 HostPath&#x000A;&#x000A;上节课提到，EmptyDir中数据不会被持久化，它会随着Pod的结束而销毁，如果想简单的将数据持久化到主机中，可以选择HostPath。&#x000A;&#x000A;HostPath就是将Node主机中一个实际目录挂在到Pod中，以供容器使用，这样的设计就可以保证Pod销毁了，但是数据依据可以存在于Node主机上。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200413214031331.png)&#x000A;&#x000A;创建一个volume-hostpath.yaml：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: volume-hostpath&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    ports:&#x000A;    - containerPort: 80&#x000A;    volumeMounts:&#x000A;    - name: logs-volume&#x000A;      mountPath: /var/log/nginx&#x000A;  - name: busybox&#x000A;    image: busybox:1.30&#x000A;    command: [&quot;/bin/sh&quot;,&quot;-c&quot;,&quot;tail -f /logs/access.log&quot;]&#x000A;    volumeMounts:&#x000A;    - name: logs-volume&#x000A;      mountPath: /logs&#x000A;  volumes:&#x000A;  - name: logs-volume&#x000A;    hostPath: &#x000A;      path: /root/logs&#x000A;      type: DirectoryOrCreate  # 目录存在就使用，不存在就先创建后使用&#x000A;```&#x000A;&#x000A;```&#x000A;关于type的值的一点说明：&#x000A;    DirectoryOrCreate 目录存在就使用，不存在就先创建后使用&#x000A;    Directory   目录必须存在&#x000A;    FileOrCreate  文件存在就使用，不存在就先创建后使用&#x000A;    File 文件必须存在 &#x000A;    Socket  unix套接字必须存在&#x000A;    CharDevice  字符设备必须存在&#x000A;    BlockDevice 块设备必须存在&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f volume-hostpath.yaml&#x000A;pod/volume-hostpath created&#x000A;&#x000A;# 查看Pod&#x000A;[root@k8s-master01 ~]# kubectl get pods volume-hostpath -n dev -o wide&#x000A;NAME                  READY   STATUS    RESTARTS   AGE   IP             NODE   ......&#x000A;pod-volume-hostpath   2/2     Running   0          16s   10.42.2.10     node1  ......&#x000A;&#x000A;#访问nginx&#x000A;[root@k8s-master01 ~]# curl 10.42.2.10&#x000A;&#x000A;[root@k8s-master01 ~]# kubectl logs -f volume-emptydir -n dev -c busybox&#x000A;&#x000A;# 接下来就可以去host的/root/logs目录下查看存储的文件了&#x000A;###  注意: 下面的操作需要到Pod所在的节点运行（案例中是node1）&#x000A;[root@node1 ~]# ls /root/logs/&#x000A;access.log  error.log&#x000A;&#x000A;# 同样的道理，如果在此目录下创建一个文件，到容器中也是可以看到的&#x000A;```&#x000A;&#x000A;##### 8.1.3 NFS&#x000A;&#x000A;HostPath可以解决数据持久化的问题，但是一旦Node节点故障了，Pod如果转移到了别的节点，又会出现问题了，此时需要准备单独的网络存储系统，比较常用的用NFS、CIFS。&#x000A;&#x000A;NFS是一个网络文件存储系统，可以搭建一台NFS服务器，然后将Pod中的存储直接连接到NFS系统上，这样的话，无论Pod在节点上怎么转移，只要Node跟NFS的对接没问题，数据就可以成功访问。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200413215133559.png)&#x000A;&#x000A;1）首先要准备nfs的服务器，这里为了简单，直接是master节点做nfs服务器&#x000A;&#x000A;```shell&#x000A;# 在nfs上安装nfs服务&#x000A;[root@nfs ~]# yum install nfs-utils -y&#x000A;&#x000A;# 准备一个共享目录&#x000A;[root@nfs ~]# mkdir /root/data/nfs -pv&#x000A;&#x000A;# 将共享目录以读写权限暴露给192.168.5.0/24网段中的所有主机&#x000A;[root@nfs ~]# vim /etc/exports&#x000A;[root@nfs ~]# more /etc/exports&#x000A;/root/data/nfs     192.168.5.0/24(rw,no_root_squash)&#x000A;&#x000A;# 启动nfs服务&#x000A;[root@nfs ~]# systemctl restart nfs&#x000A;```&#x000A;&#x000A;2）接下来，要在的每个node节点上都安装下nfs，这样的目的是为了node节点可以驱动nfs设备&#x000A;&#x000A;```shell&#x000A;# 在node上安装nfs服务，注意不需要启动&#x000A;[root@k8s-master01 ~]# yum install nfs-utils -y&#x000A;```&#x000A;&#x000A;3）接下来，就可以编写pod的配置文件了，创建volume-nfs.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: volume-nfs&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    ports:&#x000A;    - containerPort: 80&#x000A;    volumeMounts:&#x000A;    - name: logs-volume&#x000A;      mountPath: /var/log/nginx&#x000A;  - name: busybox&#x000A;    image: busybox:1.30&#x000A;    command: [&quot;/bin/sh&quot;,&quot;-c&quot;,&quot;tail -f /logs/access.log&quot;] &#x000A;    volumeMounts:&#x000A;    - name: logs-volume&#x000A;      mountPath: /logs&#x000A;  volumes:&#x000A;  - name: logs-volume&#x000A;    nfs:&#x000A;      server: 192.168.5.6  #nfs服务器地址&#x000A;      path: /root/data/nfs #共享文件路径&#x000A;```&#x000A;&#x000A;4）最后，运行下pod，观察结果&#x000A;&#x000A;```shell&#x000A;# 创建pod&#x000A;[root@k8s-master01 ~]# kubectl create -f volume-nfs.yaml&#x000A;pod/volume-nfs created&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pods volume-nfs -n dev&#x000A;NAME                  READY   STATUS    RESTARTS   AGE&#x000A;volume-nfs        2/2     Running   0          2m9s&#x000A;&#x000A;# 查看nfs服务器上的共享目录，发现已经有文件了&#x000A;[root@k8s-master01 ~]# ls /root/data/&#x000A;access.log  error.log&#x000A;```&#x000A;&#x000A;#### 8.2 高级存储&#x000A;&#x000A;前面已经学习了使用NFS提供存储，此时就要求用户会搭建NFS系统，并且会在yaml配置nfs。由于kubernetes支持的存储系统有很多，要求客户全都掌握，显然不现实。为了能够屏蔽底层存储实现的细节，方便用户使用， kubernetes引入PV和PVC两种资源对象。&#x000A;&#x000A;- PV（Persistent Volume）是持久化卷的意思，是对底层的共享存储的一种抽象。一般情况下PV由kubernetes管理员进行创建和配置，它与底层具体的共享存储技术有关，并通过插件完成与共享存储的对接。&#x000A;&#x000A;- PVC（Persistent Volume Claim）是持久卷声明的意思，是用户对于存储需求的一种声明。换句话说，PVC其实就是用户向kubernetes系统发出的一种资源需求申请。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200514194111567.png)&#x000A;&#x000A;使用了PV和PVC之后，工作可以得到进一步的细分：&#x000A;&#x000A;- 存储：存储工程师维护&#x000A;- PV： kubernetes管理员维护&#x000A;- PVC：kubernetes用户维护&#x000A;&#x000A;##### 8.2.1 PV&#x000A;&#x000A;PV是存储资源的抽象，下面是资源清单文件:&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1  &#x000A;kind: PersistentVolume&#x000A;metadata:&#x000A;  name: pv2&#x000A;spec:&#x000A;  nfs: # 存储类型，与底层真正存储对应&#x000A;  capacity:  # 存储能力，目前只支持存储空间的设置&#x000A;    storage: 2Gi&#x000A;  accessModes:  # 访问模式&#x000A;  storageClassName: # 存储类别&#x000A;  persistentVolumeReclaimPolicy: # 回收策略&#x000A;```&#x000A;&#x000A;PV 的关键配置参数说明：&#x000A;&#x000A;- **存储类型**&#x000A;&#x000A;  底层实际存储的类型，kubernetes支持多种存储类型，每种存储类型的配置都有所差异&#x000A;&#x000A;- **存储能力（capacity）**&#x000A;&#x000A;目前只支持存储空间的设置( storage=1Gi )，不过未来可能会加入IOPS、吞吐量等指标的配置&#x000A;&#x000A;- **访问模式（accessModes）**&#x000A;&#x000A;  用于描述用户应用对存储资源的访问权限，访问权限包括下面几种方式：&#x000A;&#x000A;  - ReadWriteOnce（RWO）：读写权限，但是只能被单个节点挂载&#x000A;  - ReadOnlyMany（ROX）： 只读权限，可以被多个节点挂载&#x000A;  - ReadWriteMany（RWX）：读写权限，可以被多个节点挂载&#x000A;&#x000A;  `需要注意的是，底层不同的存储类型可能支持的访问模式不同`&#x000A;&#x000A;- **回收策略（persistentVolumeReclaimPolicy）**&#x000A;&#x000A;  当PV不再被使用了之后，对其的处理方式。目前支持三种策略：&#x000A;&#x000A;  - Retain （保留） 保留数据，需要管理员手工清理数据&#x000A;  - Recycle（回收） 清除 PV 中的数据，效果相当于执行 rm -rf /thevolume/*&#x000A;  - Delete （删除） 与 PV 相连的后端存储完成 volume 的删除操作，当然这常见于云服务商的存储服务&#x000A;&#x000A;  `需要注意的是，底层不同的存储类型可能支持的回收策略不同`&#x000A;&#x000A;- **存储类别**&#x000A;&#x000A;  PV可以通过storageClassName参数指定一个存储类别&#x000A;&#x000A;  - 具有特定类别的PV只能与请求了该类别的PVC进行绑定&#x000A;  - 未设定类别的PV则只能与不请求任何类别的PVC进行绑定&#x000A;&#x000A;- **状态（status）**&#x000A;&#x000A;  一个 PV 的生命周期中，可能会处于4中不同的阶段：&#x000A;&#x000A;  - Available（可用）： 表示可用状态，还未被任何 PVC 绑定&#x000A;  - Bound（已绑定）： 表示 PV 已经被 PVC 绑定&#x000A;  - Released（已释放）： 表示 PVC 被删除，但是资源还未被集群重新声明&#x000A;  - Failed（失败）： 表示该 PV 的自动回收失败&#x000A;&#x000A;**实验**&#x000A;&#x000A;使用NFS作为存储，来演示PV的使用，创建3个PV，对应NFS中的3个暴露的路径。&#x000A;&#x000A;1) 准备NFS环境&#x000A;&#x000A;```shell&#x000A;# 创建目录&#x000A;[root@nfs ~]# mkdir /root/data/{pv1,pv2,pv3} -pv&#x000A;&#x000A;# 暴露服务&#x000A;[root@nfs ~]# more /etc/exports&#x000A;/root/data/pv1     192.168.5.0/24(rw,no_root_squash)&#x000A;/root/data/pv2     192.168.5.0/24(rw,no_root_squash)&#x000A;/root/data/pv3     192.168.5.0/24(rw,no_root_squash)&#x000A;&#x000A;# 重启服务&#x000A;[root@nfs ~]#  systemctl restart nfs&#x000A;```&#x000A;&#x000A;2) 创建pv.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: PersistentVolume&#x000A;metadata:&#x000A;  name:  pv1&#x000A;spec:&#x000A;  capacity: &#x000A;    storage: 1Gi&#x000A;  accessModes:&#x000A;  - ReadWriteMany&#x000A;  persistentVolumeReclaimPolicy: Retain&#x000A;  nfs:&#x000A;    path: /root/data/pv1&#x000A;    server: 192.168.5.6&#x000A;&#x000A;---&#x000A;&#x000A;apiVersion: v1&#x000A;kind: PersistentVolume&#x000A;metadata:&#x000A;  name:  pv2&#x000A;spec:&#x000A;  capacity: &#x000A;    storage: 2Gi&#x000A;  accessModes:&#x000A;  - ReadWriteMany&#x000A;  persistentVolumeReclaimPolicy: Retain&#x000A;  nfs:&#x000A;    path: /root/data/pv2&#x000A;    server: 192.168.5.6&#x000A;    &#x000A;---&#x000A;&#x000A;apiVersion: v1&#x000A;kind: PersistentVolume&#x000A;metadata:&#x000A;  name:  pv3&#x000A;spec:&#x000A;  capacity: &#x000A;    storage: 3Gi&#x000A;  accessModes:&#x000A;  - ReadWriteMany&#x000A;  persistentVolumeReclaimPolicy: Retain&#x000A;  nfs:&#x000A;    path: /root/data/pv3&#x000A;    server: 192.168.5.6&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建 pv&#x000A;[root@k8s-master01 ~]# kubectl create -f pv.yaml&#x000A;persistentvolume/pv1 created&#x000A;persistentvolume/pv2 created&#x000A;persistentvolume/pv3 created&#x000A;&#x000A;# 查看pv&#x000A;[root@k8s-master01 ~]# kubectl get pv -o wide&#x000A;NAME   CAPACITY   ACCESS MODES  RECLAIM POLICY  STATUS      AGE   VOLUMEMODE&#x000A;pv1    1Gi        RWX            Retain        Available    10s   Filesystem&#x000A;pv2    2Gi        RWX            Retain        Available    10s   Filesystem&#x000A;pv3    3Gi        RWX            Retain        Available    9s    Filesystem&#x000A;```&#x000A;&#x000A;##### 8.2.2 PVC&#x000A;&#x000A;PVC是资源的申请，用来声明对存储空间、访问模式、存储类别需求信息。下面是资源清单文件:&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: PersistentVolumeClaim&#x000A;metadata:&#x000A;  name: pvc&#x000A;  namespace: dev&#x000A;spec:&#x000A;  accessModes: # 访问模式&#x000A;  selector: # 采用标签对PV选择&#x000A;  storageClassName: # 存储类别&#x000A;  resources: # 请求空间&#x000A;    requests:&#x000A;      storage: 5Gi&#x000A;```&#x000A;&#x000A;PVC 的关键配置参数说明：&#x000A;&#x000A;- **访问模式（accessModes）**&#x000A;&#x000A;用于描述用户应用对存储资源的访问权限&#x000A;&#x000A;- **选择条件（selector）**&#x000A;&#x000A;  通过Label Selector的设置，可使PVC对于系统中己存在的PV进行筛选&#x000A;&#x000A;- **存储类别（storageClassName）**&#x000A;&#x000A;  PVC在定义时可以设定需要的后端存储的类别，只有设置了该class的pv才能被系统选出&#x000A;&#x000A;- **资源请求（Resources ）**&#x000A;&#x000A;  描述对存储资源的请求&#x000A;&#x000A;**实验**&#x000A;&#x000A;1) 创建pvc.yaml，申请pv&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: PersistentVolumeClaim&#x000A;metadata:&#x000A;  name: pvc1&#x000A;  namespace: dev&#x000A;spec:&#x000A;  accessModes: &#x000A;  - ReadWriteMany&#x000A;  resources:&#x000A;    requests:&#x000A;      storage: 1Gi&#x000A;---&#x000A;apiVersion: v1&#x000A;kind: PersistentVolumeClaim&#x000A;metadata:&#x000A;  name: pvc2&#x000A;  namespace: dev&#x000A;spec:&#x000A;  accessModes: &#x000A;  - ReadWriteMany&#x000A;  resources:&#x000A;    requests:&#x000A;      storage: 1Gi&#x000A;---&#x000A;apiVersion: v1&#x000A;kind: PersistentVolumeClaim&#x000A;metadata:&#x000A;  name: pvc3&#x000A;  namespace: dev&#x000A;spec:&#x000A;  accessModes: &#x000A;  - ReadWriteMany&#x000A;  resources:&#x000A;    requests:&#x000A;      storage: 1Gi&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建pvc&#x000A;[root@k8s-master01 ~]# kubectl create -f pvc.yaml&#x000A;persistentvolumeclaim/pvc1 created&#x000A;persistentvolumeclaim/pvc2 created&#x000A;persistentvolumeclaim/pvc3 created&#x000A;&#x000A;# 查看pvc&#x000A;[root@k8s-master01 ~]# kubectl get pvc  -n dev -o wide&#x000A;NAME   STATUS   VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE   VOLUMEMODE&#x000A;pvc1   Bound    pv1      1Gi        RWX                           15s   Filesystem&#x000A;pvc2   Bound    pv2      2Gi        RWX                           15s   Filesystem&#x000A;pvc3   Bound    pv3      3Gi        RWX                           15s   Filesystem&#x000A;&#x000A;# 查看pv&#x000A;[root@k8s-master01 ~]# kubectl get pv -o wide&#x000A;NAME  CAPACITY ACCESS MODES  RECLAIM POLICY  STATUS    CLAIM       AGE     VOLUMEMODE&#x000A;pv1    1Gi        RWx        Retain          Bound    dev/pvc1    3h37m    Filesystem&#x000A;pv2    2Gi        RWX        Retain          Bound    dev/pvc2    3h37m    Filesystem&#x000A;pv3    3Gi        RWX        Retain          Bound    dev/pvc3    3h37m    Filesystem   &#x000A;```&#x000A;&#x000A;2) 创建pods.yaml, 使用pv&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod1&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: busybox&#x000A;    image: busybox:1.30&#x000A;    command: [&quot;/bin/sh&quot;,&quot;-c&quot;,&quot;while true;do echo pod1 &gt;&gt; /root/out.txt; sleep 10; done;&quot;]&#x000A;    volumeMounts:&#x000A;    - name: volume&#x000A;      mountPath: /root/&#x000A;  volumes:&#x000A;    - name: volume&#x000A;      persistentVolumeClaim:&#x000A;        claimName: pvc1&#x000A;        readOnly: false&#x000A;---&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod2&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: busybox&#x000A;    image: busybox:1.30&#x000A;    command: [&quot;/bin/sh&quot;,&quot;-c&quot;,&quot;while true;do echo pod2 &gt;&gt; /root/out.txt; sleep 10; done;&quot;]&#x000A;    volumeMounts:&#x000A;    - name: volume&#x000A;      mountPath: /root/&#x000A;  volumes:&#x000A;    - name: volume&#x000A;      persistentVolumeClaim:&#x000A;        claimName: pvc2&#x000A;        readOnly: false&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pods.yaml&#x000A;pod/pod1 created&#x000A;pod/pod2 created&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -o wide&#x000A;NAME   READY   STATUS    RESTARTS   AGE   IP            NODE   &#x000A;pod1   1/1     Running   0          14s   10.244.1.69   node1   &#x000A;pod2   1/1     Running   0          14s   10.244.1.70   node1  &#x000A;&#x000A;# 查看pvc&#x000A;[root@k8s-master01 ~]# kubectl get pvc -n dev -o wide&#x000A;NAME   STATUS   VOLUME   CAPACITY   ACCESS MODES      AGE   VOLUMEMODE&#x000A;pvc1   Bound    pv1      1Gi        RWX               94m   Filesystem&#x000A;pvc2   Bound    pv2      2Gi        RWX               94m   Filesystem&#x000A;pvc3   Bound    pv3      3Gi        RWX               94m   Filesystem&#x000A;&#x000A;# 查看pv&#x000A;[root@k8s-master01 ~]# kubectl get pv -n dev -o wide&#x000A;NAME   CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM       AGE     VOLUMEMODE&#x000A;pv1    1Gi        RWX            Retain           Bound    dev/pvc1    5h11m   Filesystem&#x000A;pv2    2Gi        RWX            Retain           Bound    dev/pvc2    5h11m   Filesystem&#x000A;pv3    3Gi        RWX            Retain           Bound    dev/pvc3    5h11m   Filesystem&#x000A;&#x000A;# 查看nfs中的文件存储&#x000A;[root@nfs ~]# more /root/data/pv1/out.txt&#x000A;node1&#x000A;node1&#x000A;[root@nfs ~]# more /root/data/pv2/out.txt&#x000A;node2&#x000A;node2&#x000A;```&#x000A;&#x000A;##### 8.2.3 生命周期&#x000A;&#x000A;PVC和PV是一一对应的，PV和PVC之间的相互作用遵循以下生命周期：&#x000A;&#x000A;- **资源供应**：管理员手动创建底层存储和PV&#x000A;&#x000A;- **资源绑定**：用户创建PVC，kubernetes负责根据PVC的声明去寻找PV，并绑定&#x000A;&#x000A;  在用户定义好PVC之后，系统将根据PVC对存储资源的请求在已存在的PV中选择一个满足条件的&#x000A;&#x000A;  - 一旦找到，就将该PV与用户定义的PVC进行绑定，用户的应用就可以使用这个PVC了&#x000A;  - 如果找不到，PVC则会无限期处于Pending状态，直到等到系统管理员创建了一个符合其要求的PV&#x000A;&#x000A;  PV一旦绑定到某个PVC上，就会被这个PVC独占，不能再与其他PVC进行绑定了&#x000A;&#x000A;- **资源使用**：用户可在pod中像volume一样使用pvc&#x000A;&#x000A;  Pod使用Volume的定义，将PVC挂载到容器内的某个路径进行使用。&#x000A;&#x000A;- **资源释放**：用户删除pvc来释放pv&#x000A;&#x000A;  当存储资源使用完毕后，用户可以删除PVC，与该PVC绑定的PV将会被标记为“已释放”，但还不能立刻与其他PVC进行绑定。通过之前PVC写入的数据可能还被留在存储设备上，只有在清除之后该PV才能再次使用。&#x000A;&#x000A;- **资源回收**：kubernetes根据pv设置的回收策略进行资源的回收&#x000A;&#x000A;  对于PV，管理员可以设定回收策略，用于设置与之绑定的PVC释放资源之后如何处理遗留数据的问题。只有PV的存储空间完成回收，才能供新的PVC绑定和使用&#x000A;&#x000A;![img](Kubenetes.assets/image-20200515002806726.png)&#x000A;&#x000A;#### 8.3 配置存储&#x000A;&#x000A;##### 8.3.1 ConfigMap&#x000A;&#x000A;ConfigMap是一种比较特殊的存储卷，它的主要作用是用来存储配置信息的。&#x000A;&#x000A;创建configmap.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: ConfigMap&#x000A;metadata:&#x000A;  name: configmap&#x000A;  namespace: dev&#x000A;data:&#x000A;  info: |&#x000A;    username:admin&#x000A;    password:123456&#x000A;```&#x000A;&#x000A;接下来，使用此配置文件创建configmap&#x000A;&#x000A;```shell&#x000A;# 创建configmap&#x000A;[root@k8s-master01 ~]# kubectl create -f configmap.yaml&#x000A;configmap/configmap created&#x000A;&#x000A;# 查看configmap详情&#x000A;[root@k8s-master01 ~]# kubectl describe cm configmap -n dev&#x000A;Name:         configmap&#x000A;Namespace:    dev&#x000A;Labels:       &lt;none&gt;&#x000A;Annotations:  &lt;none&gt;&#x000A;&#x000A;Data&#x000A;====&#x000A;info:&#x000A;----&#x000A;username:admin&#x000A;password:123456&#x000A;&#x000A;Events:  &lt;none&gt;&#x000A;```&#x000A;&#x000A;接下来创建一个pod-configmap.yaml，将上面创建的configmap挂载进去&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-configmap&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    volumeMounts: # 将configmap挂载到目录&#x000A;    - name: config&#x000A;      mountPath: /configmap/config&#x000A;  volumes: # 引用configmap&#x000A;  - name: config&#x000A;    configMap:&#x000A;      name: configmap&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-configmap.yaml&#x000A;pod/pod-configmap created&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pod pod-configmap -n dev&#x000A;NAME            READY   STATUS    RESTARTS   AGE&#x000A;pod-configmap   1/1     Running   0          6s&#x000A;&#x000A;#进入容器&#x000A;[root@k8s-master01 ~]# kubectl exec -it pod-configmap -n dev /bin/sh&#x000A;# cd /configmap/config/&#x000A;# ls&#x000A;info&#x000A;# more info&#x000A;username:admin&#x000A;password:123456&#x000A;&#x000A;# 可以看到映射已经成功，每个configmap都映射成了一个目录&#x000A;# key---&gt;文件     value----&gt;文件中的内容&#x000A;# 此时如果更新configmap的内容, 容器中的值也会动态更新&#x000A;```&#x000A;&#x000A;##### 8.3.2 Secret&#x000A;&#x000A;在kubernetes中，还存在一种和ConfigMap非常类似的对象，称为Secret对象。它主要用于存储敏感信息，例如密码、秘钥、证书等等。&#x000A;&#x000A;1) 首先使用base64对数据进行编码&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# echo -n &#39;admin&#39; | base64 #准备username&#x000A;YWRtaW4=&#x000A;[root@k8s-master01 ~]# echo -n &#39;123456&#39; | base64 #准备password&#x000A;MTIzNDU2&#x000A;```&#x000A;&#x000A;2) 接下来编写secret.yaml，并创建Secret&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Secret&#x000A;metadata:&#x000A;  name: secret&#x000A;  namespace: dev&#x000A;type: Opaque&#x000A;data:&#x000A;  username: YWRtaW4=&#x000A;  password: MTIzNDU2&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建secret&#x000A;[root@k8s-master01 ~]# kubectl create -f secret.yaml&#x000A;secret/secret created&#x000A;&#x000A;# 查看secret详情&#x000A;[root@k8s-master01 ~]# kubectl describe secret secret -n dev&#x000A;Name:         secret&#x000A;Namespace:    dev&#x000A;Labels:       &lt;none&gt;&#x000A;Annotations:  &lt;none&gt;&#x000A;Type:  Opaque&#x000A;Data&#x000A;====&#x000A;password:  6 bytes&#x000A;username:  5 bytes&#x000A;```&#x000A;&#x000A;3) 创建pod-secret.yaml，将上面创建的secret挂载进去：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-secret&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    volumeMounts: # 将secret挂载到目录&#x000A;    - name: config&#x000A;      mountPath: /secret/config&#x000A;  volumes:&#x000A;  - name: config&#x000A;    secret:&#x000A;      secretName: secret&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-secret.yaml&#x000A;pod/pod-secret created&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pod pod-secret -n dev&#x000A;NAME            READY   STATUS    RESTARTS   AGE&#x000A;pod-secret      1/1     Running   0          2m28s&#x000A;&#x000A;# 进入容器，查看secret信息，发现已经自动解码了&#x000A;[root@k8s-master01 ~]# kubectl exec -it pod-secret /bin/sh -n dev&#x000A;/ # ls /secret/config/&#x000A;password  username&#x000A;/ # more /secret/config/username&#x000A;admin&#x000A;/ # more /secret/config/password&#x000A;123456&#x000A;```&#x000A;&#x000A;至此，已经实现了利用secret实现了信息的编码。&#x000A;&#x000A;### 9. 安全认证&#x000A;&#x000A;#### 9.1 访问控制概述&#x000A;&#x000A;Kubernetes作为一个分布式集群的管理工具，保证集群的安全性是其一个重要的任务。所谓的安全性其实就是保证对Kubernetes的各种**客户端**进行**认证和鉴权**操作。&#x000A;&#x000A;**客户端**&#x000A;&#x000A;在Kubernetes集群中，客户端通常有两类：&#x000A;&#x000A;- **User Account**：一般是独立于kubernetes之外的其他服务管理的用户账号。&#x000A;- **Service Account**：kubernetes管理的账号，用于为Pod中的服务进程在访问Kubernetes时提供身份标识。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200520102949189.png)&#x000A;&#x000A;**认证、授权与准入控制**&#x000A;&#x000A;ApiServer是访问及管理资源对象的唯一入口。任何一个请求访问ApiServer，都要经过下面三个流程：&#x000A;&#x000A;- Authentication（认证）：身份鉴别，只有正确的账号才能够通过认证&#x000A;- Authorization（授权）： 判断用户是否有权限对访问的资源执行特定的动作&#x000A;- Admission Control（准入控制）：用于补充授权机制以实现更加精细的访问控制功能。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200520103942580.png)&#x000A;&#x000A;#### 9.2 认证管理&#x000A;&#x000A;Kubernetes集群安全的最关键点在于如何识别并认证客户端身份，它提供了3种客户端身份认证方式：&#x000A;&#x000A;- HTTP Base认证：通过用户名+密码的方式认证&#x000A;&#x000A;  ```&#x000A;      这种认证方式是把“用户名:密码”用BASE64算法进行编码后的字符串放在HTTP请求中的Header Authorization域里发送给服务端。服务端收到后进行解码，获取用户名及密码，然后进行用户身份认证的过程。&#x000A;  ```&#x000A;&#x000A;- HTTP Token认证：通过一个Token来识别合法用户&#x000A;&#x000A;  ```&#x000A;      这种认证方式是用一个很长的难以被模仿的字符串--Token来表明客户身份的一种方式。每个Token对应一个用户名，当客户端发起API调用请求时，需要在HTTP Header里放入Token，API Server接到Token后会跟服务器中保存的token进行比对，然后进行用户身份认证的过程。&#x000A;  ```&#x000A;&#x000A;- HTTPS证书认证：基于CA根证书签名的双向数字证书认证方式&#x000A;&#x000A;  ```&#x000A;      这种认证方式是安全性最高的一种方式，但是同时也是操作起来最麻烦的一种方式。&#x000A;  ```&#x000A;&#x000A;![img](Kubenetes.assets/image-20200518211037434.png)&#x000A;&#x000A;**HTTPS认证大体分为3个过程：**&#x000A;&#x000A;1. 证书申请和下发&#x000A;&#x000A;   ```&#x000A;     HTTPS通信双方的服务器向CA机构申请证书，CA机构下发根证书、服务端证书及私钥给申请者&#x000A;   ```&#x000A;&#x000A;2. 客户端和服务端的双向认证&#x000A;&#x000A;   ```&#x000A;     1&gt; 客户端向服务器端发起请求，服务端下发自己的证书给客户端，&#x000A;        客户端接收到证书后，通过私钥解密证书，在证书中获得服务端的公钥，&#x000A;        客户端利用服务器端的公钥认证证书中的信息，如果一致，则认可这个服务器&#x000A;     2&gt; 客户端发送自己的证书给服务器端，服务端接收到证书后，通过私钥解密证书，&#x000A;        在证书中获得客户端的公钥，并用该公钥认证证书信息，确认客户端是否合法&#x000A;   ```&#x000A;&#x000A;3. 服务器端和客户端进行通信&#x000A;&#x000A;   ```&#x000A;     服务器端和客户端协商好加密方案后，客户端会产生一个随机的秘钥并加密，然后发送到服务器端。&#x000A;     服务器端接收这个秘钥后，双方接下来通信的所有内容都通过该随机秘钥加密&#x000A;   ```&#x000A;&#x000A;&gt; 注意: Kubernetes允许同时配置多种认证方式，只要其中任意一个方式认证通过即可&#x000A;&#x000A;#### 9.3 授权管理&#x000A;&#x000A;授权发生在认证成功之后，通过认证就可以知道请求用户是谁， 然后Kubernetes会根据事先定义的授权策略来决定用户是否有权限访问，这个过程就称为授权。&#x000A;&#x000A;每个发送到ApiServer的请求都带上了用户和资源的信息：比如发送请求的用户、请求的路径、请求的动作等，授权就是根据这些信息和授权策略进行比较，如果符合策略，则认为授权通过，否则会返回错误。&#x000A;&#x000A;API Server目前支持以下几种授权策略：&#x000A;&#x000A;- AlwaysDeny：表示拒绝所有请求，一般用于测试&#x000A;- AlwaysAllow：允许接收所有请求，相当于集群不需要授权流程（Kubernetes默认的策略）&#x000A;- ABAC：基于属性的访问控制，表示使用用户配置的授权规则对用户请求进行匹配和控制&#x000A;- Webhook：通过调用外部REST服务对用户进行授权&#x000A;- Node：是一种专用模式，用于对kubelet发出的请求进行访问控制&#x000A;- RBAC：基于角色的访问控制（kubeadm安装方式下的默认选项）&#x000A;&#x000A;RBAC(Role-Based Access Control) 基于角色的访问控制，主要是在描述一件事情：**给哪些对象授予了哪些权限**&#x000A;&#x000A;其中涉及到了下面几个概念：&#x000A;&#x000A;- 对象：User、Groups、ServiceAccount&#x000A;- 角色：代表着一组定义在资源上的可操作动作(权限)的集合&#x000A;- 绑定：将定义好的角色跟用户绑定在一起&#x000A;&#x000A;![img](Kubenetes.assets/image-20200519181209566.png)&#x000A;&#x000A;RBAC引入了4个顶级资源对象：&#x000A;&#x000A;- Role、ClusterRole：角色，用于指定一组权限&#x000A;- RoleBinding、ClusterRoleBinding：角色绑定，用于将角色（权限）赋予给对象&#x000A;&#x000A;**Role、ClusterRole**&#x000A;&#x000A;一个角色就是一组权限的集合，这里的权限都是许可形式的（白名单）。&#x000A;&#x000A;```yaml&#x000A;# Role只能对命名空间内的资源进行授权，需要指定nameapce&#x000A;kind: Role&#x000A;apiVersion: rbac.authorization.k8s.io/v1beta1&#x000A;metadata:&#x000A;  namespace: dev&#x000A;  name: authorization-role&#x000A;rules:&#x000A;- apiGroups: [&quot;&quot;]  # 支持的API组列表,&quot;&quot; 空字符串，表示核心API群&#x000A;  resources: [&quot;pods&quot;] # 支持的资源对象列表&#x000A;  verbs: [&quot;get&quot;, &quot;watch&quot;, &quot;list&quot;] # 允许的对资源对象的操作方法列表&#x000A;```&#x000A;&#x000A;```yaml&#x000A;# ClusterRole可以对集群范围内资源、跨namespaces的范围资源、非资源类型进行授权&#x000A;kind: ClusterRole&#x000A;apiVersion: rbac.authorization.k8s.io/v1beta1&#x000A;metadata:&#x000A; name: authorization-clusterrole&#x000A;rules:&#x000A;- apiGroups: [&quot;&quot;]&#x000A;  resources: [&quot;pods&quot;]&#x000A;  verbs: [&quot;get&quot;, &quot;watch&quot;, &quot;list&quot;]&#x000A;```&#x000A;&#x000A;需要详细说明的是，rules中的参数：&#x000A;&#x000A;- apiGroups: 支持的API组列表&#x000A;&#x000A;  ```bash&#x000A;  &quot;&quot;,&quot;apps&quot;, &quot;autoscaling&quot;, &quot;batch&quot;&#x000A;  ```&#x000A;&#x000A;- resources：支持的资源对象列表&#x000A;&#x000A;  ```bash&#x000A;  &quot;services&quot;, &quot;endpoints&quot;, &quot;pods&quot;,&quot;secrets&quot;,&quot;configmaps&quot;,&quot;crontabs&quot;,&quot;deployments&quot;,&quot;jobs&quot;,&#x000A;  &quot;nodes&quot;,&quot;rolebindings&quot;,&quot;clusterroles&quot;,&quot;daemonsets&quot;,&quot;replicasets&quot;,&quot;statefulsets&quot;,&#x000A;  &quot;horizontalpodautoscalers&quot;,&quot;replicationcontrollers&quot;,&quot;cronjobs&quot;&#x000A;  ```&#x000A;&#x000A;- verbs：对资源对象的操作方法列表&#x000A;&#x000A;  ```bash&#x000A;  &quot;get&quot;, &quot;list&quot;, &quot;watch&quot;, &quot;create&quot;, &quot;update&quot;, &quot;patch&quot;, &quot;delete&quot;, &quot;exec&quot;&#x000A;  ```&#x000A;&#x000A;**RoleBinding、ClusterRoleBinding**&#x000A;&#x000A;角色绑定用来把一个角色绑定到一个目标对象上，绑定目标可以是User、Group或者ServiceAccount。&#x000A;&#x000A;```yaml&#x000A;# RoleBinding可以将同一namespace中的subject绑定到某个Role下，则此subject即具有该Role定义的权限&#x000A;kind: RoleBinding&#x000A;apiVersion: rbac.authorization.k8s.io/v1beta1&#x000A;metadata:&#x000A;  name: authorization-role-binding&#x000A;  namespace: dev&#x000A;subjects:&#x000A;- kind: User&#x000A;  name: heima&#x000A;  apiGroup: rbac.authorization.k8s.io&#x000A;roleRef:&#x000A;  kind: Role&#x000A;  name: authorization-role&#x000A;  apiGroup: rbac.authorization.k8s.io&#x000A;```&#x000A;&#x000A;```yaml&#x000A;# ClusterRoleBinding在整个集群级别和所有namespaces将特定的subject与ClusterRole绑定，授予权限&#x000A;kind: ClusterRoleBinding&#x000A;apiVersion: rbac.authorization.k8s.io/v1beta1&#x000A;metadata:&#x000A; name: authorization-clusterrole-binding&#x000A;subjects:&#x000A;- kind: User&#x000A;  name: heima&#x000A;  apiGroup: rbac.authorization.k8s.io&#x000A;roleRef:&#x000A;  kind: ClusterRole&#x000A;  name: authorization-clusterrole&#x000A;  apiGroup: rbac.authorization.k8s.io&#x000A;```&#x000A;&#x000A;**RoleBinding引用ClusterRole进行授权**&#x000A;&#x000A;RoleBinding可以引用ClusterRole，对属于同一命名空间内ClusterRole定义的资源主体进行授权。&#x000A;&#x000A;```&#x000A;    一种很常用的做法就是，集群管理员为集群范围预定义好一组角色（ClusterRole），然后在多个命名空间中重复使用这些ClusterRole。这样可以大幅提高授权管理工作效率，也使得各个命名空间下的基础性授权规则与使用体验保持一致。&#x000A;```&#x000A;&#x000A;```yaml&#x000A;# 虽然authorization-clusterrole是一个集群角色，但是因为使用了RoleBinding&#x000A;# 所以heima只能读取dev命名空间中的资源&#x000A;kind: RoleBinding&#x000A;apiVersion: rbac.authorization.k8s.io/v1beta1&#x000A;metadata:&#x000A;  name: authorization-role-binding-ns&#x000A;  namespace: dev&#x000A;subjects:&#x000A;- kind: User&#x000A;  name: heima&#x000A;  apiGroup: rbac.authorization.k8s.io&#x000A;roleRef:&#x000A;  kind: ClusterRole&#x000A;  name: authorization-clusterrole&#x000A;  apiGroup: rbac.authorization.k8s.io&#x000A;```&#x000A;&#x000A;**实战：创建一个只能管理dev空间下Pods资源的账号**&#x000A;&#x000A;1) 创建账号&#x000A;&#x000A;```shell&#x000A;# 1) 创建证书&#x000A;[root@k8s-master01 pki]# cd /etc/kubernetes/pki/&#x000A;[root@k8s-master01 pki]# (umask 077;openssl genrsa -out devman.key 2048)&#x000A;&#x000A;# 2) 用apiserver的证书去签署&#x000A;# 2-1) 签名申请，申请的用户是devman,组是devgroup&#x000A;[root@k8s-master01 pki]# openssl req -new -key devman.key -out devman.csr -subj &quot;/CN=devman/O=devgroup&quot;     &#x000A;# 2-2) 签署证书&#x000A;[root@k8s-master01 pki]# openssl x509 -req -in devman.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out devman.crt -days 3650&#x000A;&#x000A;# 3) 设置集群、用户、上下文信息&#x000A;[root@k8s-master01 pki]# kubectl config set-cluster kubernetes --embed-certs=true --certificate-authority=/etc/kubernetes/pki/ca.crt --server=https://192.168.109.100:6443&#x000A;&#x000A;[root@k8s-master01 pki]# kubectl config set-credentials devman --embed-certs=true --client-certificate=/etc/kubernetes/pki/devman.crt --client-key=/etc/kubernetes/pki/devman.key&#x000A;&#x000A;[root@k8s-master01 pki]# kubectl config set-context devman@kubernetes --cluster=kubernetes --user=devman&#x000A;&#x000A;# 切换账户到devman&#x000A;[root@k8s-master01 pki]# kubectl config use-context devman@kubernetes&#x000A;Switched to context &quot;devman@kubernetes&quot;.&#x000A;&#x000A;# 查看dev下pod，发现没有权限&#x000A;[root@k8s-master01 pki]# kubectl get pods -n dev&#x000A;Error from server (Forbidden): pods is forbidden: User &quot;devman&quot; cannot list resource &quot;pods&quot; in API group &quot;&quot; in the namespace &quot;dev&quot;&#x000A;&#x000A;# 切换到admin账户&#x000A;[root@k8s-master01 pki]# kubectl config use-context kubernetes-admin@kubernetes&#x000A;Switched to context &quot;kubernetes-admin@kubernetes&quot;.&#x000A;```&#x000A;&#x000A;2） 创建Role和RoleBinding，为devman用户授权&#x000A;&#x000A;```yaml&#x000A;kind: Role&#x000A;apiVersion: rbac.authorization.k8s.io/v1beta1&#x000A;metadata:&#x000A;  namespace: dev&#x000A;  name: dev-role&#x000A;rules:&#x000A;- apiGroups: [&quot;&quot;]&#x000A;  resources: [&quot;pods&quot;]&#x000A;  verbs: [&quot;get&quot;, &quot;watch&quot;, &quot;list&quot;]&#x000A;  &#x000A;---&#x000A;&#x000A;kind: RoleBinding&#x000A;apiVersion: rbac.authorization.k8s.io/v1beta1&#x000A;metadata:&#x000A;  name: authorization-role-binding&#x000A;  namespace: dev&#x000A;subjects:&#x000A;- kind: User&#x000A;  name: devman&#x000A;  apiGroup: rbac.authorization.k8s.io&#x000A;roleRef:&#x000A;  kind: Role&#x000A;  name: dev-role&#x000A;  apiGroup: rbac.authorization.k8s.io&#x000A;```&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 pki]# kubectl create -f dev-role.yaml&#x000A;role.rbac.authorization.k8s.io/dev-role created&#x000A;rolebinding.rbac.authorization.k8s.io/authorization-role-binding created&#x000A;```&#x000A;&#x000A;3) 切换账户，再次验证&#x000A;&#x000A;```shell&#x000A;# 切换账户到devman&#x000A;[root@k8s-master01 pki]# kubectl config use-context devman@kubernetes&#x000A;Switched to context &quot;devman@kubernetes&quot;.&#x000A;&#x000A;# 再次查看&#x000A;[root@k8s-master01 pki]# kubectl get pods -n dev&#x000A;NAME                                 READY   STATUS             RESTARTS   AGE&#x000A;nginx-deployment-66cb59b984-8wp2k    1/1     Running            0          4d1h&#x000A;nginx-deployment-66cb59b984-dc46j    1/1     Running            0          4d1h&#x000A;nginx-deployment-66cb59b984-thfck    1/1     Running            0          4d1h&#x000A;&#x000A;# 为了不影响后面的学习,切回admin账户&#x000A;[root@k8s-master01 pki]# kubectl config use-context kubernetes-admin@kubernetes&#x000A;Switched to context &quot;kubernetes-admin@kubernetes&quot;.&#x000A;```&#x000A;&#x000A;#### 9.4 准入控制&#x000A;&#x000A;通过了前面的认证和授权之后，还需要经过准入控制处理通过之后，apiserver才会处理这个请求。&#x000A;&#x000A;准入控制是一个可配置的控制器列表，可以通过在Api-Server上通过命令行设置选择执行哪些准入控制器：&#x000A;&#x000A;```&#x000A;--admission-control=NamespaceLifecycle,LimitRanger,ServiceAccount,PersistentVolumeLabel,&#x000A;                      DefaultStorageClass,ResourceQuota,DefaultTolerationSeconds&#x000A;```&#x000A;&#x000A;只有当所有的准入控制器都检查通过之后，apiserver才执行该请求，否则返回拒绝。&#x000A;&#x000A;当前可配置的Admission Control准入控制如下：&#x000A;&#x000A;- AlwaysAdmit：允许所有请求&#x000A;- AlwaysDeny：禁止所有请求，一般用于测试&#x000A;- AlwaysPullImages：在启动容器之前总去下载镜像&#x000A;- DenyExecOnPrivileged：它会拦截所有想在Privileged Container上执行命令的请求&#x000A;- ImagePolicyWebhook：这个插件将允许后端的一个Webhook程序来完成admission controller的功能。&#x000A;- Service Account：实现ServiceAccount实现了自动化&#x000A;- SecurityContextDeny：这个插件将使用SecurityContext的Pod中的定义全部失效&#x000A;- ResourceQuota：用于资源配额管理目的，观察所有请求，确保在namespace上的配额不会超标&#x000A;- LimitRanger：用于资源限制管理，作用于namespace上，确保对Pod进行资源限制&#x000A;- InitialResources：为未设置资源请求与限制的Pod，根据其镜像的历史资源的使用情况进行设置&#x000A;- NamespaceLifecycle：如果尝试在一个不存在的namespace中创建资源对象，则该创建请求将被拒绝。当删除一个namespace时，系统将会删除该namespace中所有对象。&#x000A;- DefaultStorageClass：为了实现共享存储的动态供应，为未指定StorageClass或PV的PVC尝试匹配默认的StorageClass，尽可能减少用户在申请PVC时所需了解的后端存储细节&#x000A;- DefaultTolerationSeconds：这个插件为那些没有设置forgiveness tolerations并具有notready:NoExecute和unreachable:NoExecute两种taints的Pod设置默认的“容忍”时间，为5min&#x000A;- PodSecurityPolicy：这个插件用于在创建或修改Pod时决定是否根据Pod的security context和可用的PodSecurityPolicy对Pod的安全策略进行控制&#x000A;&#x000A;### 10. DashBoard&#x000A;&#x000A;之前在kubernetes中完成的所有操作都是通过命令行工具kubectl完成的。其实，为了提供更丰富的用户体验，kubernetes还开发了一个基于web的用户界面（Dashboard）。用户可以使用Dashboard部署容器化的应用，还可以监控应用的状态，执行故障排查以及管理kubernetes中各种资源。&#x000A;&#x000A;#### 10.1 部署Dashboard&#x000A;&#x000A;1) 下载yaml，并运行Dashboard&#x000A;&#x000A;```shell&#x000A;# 下载yaml&#x000A;[root@k8s-master01 ~]# wget  https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml&#x000A;&#x000A;# 修改kubernetes-dashboard的Service类型&#x000A;kind: Service&#x000A;apiVersion: v1&#x000A;metadata:&#x000A;  labels:&#x000A;    k8s-app: kubernetes-dashboard&#x000A;  name: kubernetes-dashboard&#x000A;  namespace: kubernetes-dashboard&#x000A;spec:&#x000A;  type: NodePort  # 新增&#x000A;  ports:&#x000A;    - port: 443&#x000A;      targetPort: 8443&#x000A;      nodePort: 30009  # 新增&#x000A;  selector:&#x000A;    k8s-app: kubernetes-dashboard&#x000A;&#x000A;# 部署&#x000A;[root@k8s-master01 ~]# kubectl create -f recommended.yaml&#x000A;&#x000A;# 查看namespace下的kubernetes-dashboard下的资源&#x000A;[root@k8s-master01 ~]# kubectl get pod,svc -n kubernetes-dashboard&#x000A;NAME                                            READY   STATUS    RESTARTS   AGE&#x000A;pod/dashboard-metrics-scraper-c79c65bb7-zwfvw   1/1     Running   0          111s&#x000A;pod/kubernetes-dashboard-56484d4c5-z95z5        1/1     Running   0          111s&#x000A;&#x000A;NAME                               TYPE       CLUSTER-IP      EXTERNAL-IP  PORT(S)         AGE&#x000A;service/dashboard-metrics-scraper  ClusterIP  10.96.89.218    &lt;none&gt;       8000/TCP        111s&#x000A;service/kubernetes-dashboard       NodePort   10.104.178.171  &lt;none&gt;       443:30009/TCP   111s&#x000A;```&#x000A;&#x000A;2）创建访问账户，获取token&#x000A;&#x000A;```shell&#x000A;# 创建账号&#x000A;[root@k8s-master01-1 ~]# kubectl create serviceaccount dashboard-admin -n kubernetes-dashboard&#x000A;&#x000A;# 授权&#x000A;[root@k8s-master01-1 ~]# kubectl create clusterrolebinding dashboard-admin-rb --clusterrole=cluster-admin --serviceaccount=kubernetes-dashboard:dashboard-admin&#x000A;&#x000A;# 获取账号token&#x000A;[root@k8s-master01 ~]#  kubectl get secrets -n kubernetes-dashboard | grep dashboard-admin&#x000A;dashboard-admin-token-xbqhh        kubernetes.io/service-account-token   3      2m35s&#x000A;&#x000A;[root@k8s-master01 ~]# kubectl describe secrets dashboard-admin-token-xbqhh -n kubernetes-dashboard&#x000A;Name:         dashboard-admin-token-xbqhh&#x000A;Namespace:    kubernetes-dashboard&#x000A;Labels:       &lt;none&gt;&#x000A;Annotations:  kubernetes.io/service-account.name: dashboard-admin&#x000A;              kubernetes.io/service-account.uid: 95d84d80-be7a-4d10-a2e0-68f90222d039&#x000A;&#x000A;Type:  kubernetes.io/service-account-token&#x000A;&#x000A;Data&#x000A;====&#x000A;namespace:  20 bytes&#x000A;token:      eyJhbGciOiJSUzI1NiIsImtpZCI6ImJrYkF4bW5XcDhWcmNGUGJtek5NODFuSXl1aWptMmU2M3o4LTY5a2FKS2cifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlcm5ldGVzLWRhc2hib2FyZCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJkYXNoYm9hcmQtYWRtaW4tdG9rZW4teGJxaGgiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC5uYW1lIjoiZGFzaGJvYXJkLWFkbWluIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQudWlkIjoiOTVkODRkODAtYmU3YS00ZDEwLWEyZTAtNjhmOTAyMjJkMDM5Iiwic3ViIjoic3lzdGVtOnNlcnZpY2VhY2NvdW50Omt1YmVybmV0ZXMtZGFzaGJvYXJkOmRhc2hib2FyZC1hZG1pbiJ9.NAl7e8ZfWWdDoPxkqzJzTB46sK9E8iuJYnUI9vnBaY3Jts7T1g1msjsBnbxzQSYgAG--cV0WYxjndzJY_UWCwaGPrQrt_GunxmOK9AUnzURqm55GR2RXIZtjsWVP2EBatsDgHRmuUbQvTFOvdJB4x3nXcYLN2opAaMqg3rnU2rr-A8zCrIuX_eca12wIp_QiuP3SF-tzpdLpsyRfegTJZl6YnSGyaVkC9id-cxZRb307qdCfXPfCHR_2rt5FVfxARgg_C0e3eFHaaYQO7CitxsnIoIXpOFNAR8aUrmopJyODQIPqBWUehb7FhlU1DCduHnIIXVC_UICZ-MKYewBDLw&#x000A;ca.crt:     1025 bytes&#x000A;```&#x000A;&#x000A;3）通过浏览器访问Dashboard的UI&#x000A;&#x000A;在登录页面上输入上面的token&#x000A;&#x000A;![image-20200520144548997](Kubenetes.assets/image-20200520144548997.png)&#x000A;&#x000A;出现下面的页面代表成功&#x000A;&#x000A;![image-20200520144959353](Kubenetes.assets/image-20200520144959353.png)&#x000A;&#x000A;#### 10.2 使用DashBoard&#x000A;&#x000A;本章节以Deployment为例演示DashBoard的使用&#x000A;&#x000A;**查看**&#x000A;&#x000A;选择指定的命名空间`dev`，然后点击`Deployments`，查看dev空间下的所有deployment&#x000A;&#x000A;![img](Kubenetes.assets/image-20200520154628679.png)&#x000A;&#x000A;**扩缩容**&#x000A;&#x000A;在`Deployment`上点击`规模`，然后指定`目标副本数量`，点击确定&#x000A;&#x000A;![img](Kubenetes.assets/image-20200520162605102.png)&#x000A;&#x000A;**编辑**&#x000A;&#x000A;在`Deployment`上点击`编辑`，然后修改`yaml文件`，点击确定&#x000A;&#x000A;![image-20200520163253644](Kubenetes.assets/image-20200520163253644.png)&#x000A;&#x000A;**查看Pod**&#x000A;&#x000A;点击`Pods`, 查看pods列表&#x000A;&#x000A;![img](Kubenetes.assets/image-20200520163552110.png)&#x000A;&#x000A;**操作Pod**&#x000A;&#x000A;选中某个Pod，可以对其执行日志（logs）、进入执行（exec）、编辑、删除操作&#x000A;&#x000A;&#x000A;&#x000A;&gt; Dashboard提供了kubectl的绝大部分功能，这里不再一一演示&#x000A;&#x000A;&#x000A;&#x000A;&#x000A;&#x000A;</textarea>
<a class="ui button" id="copy-text" href="#">Copy</a>
<a class="ui button edit-blob" title="Please login" href="/yooome/golang/edit/main/21-k8s%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B/Kubernetes%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B.md">Edit</a>
<a class="ui button edit-raw" target="_blank" href="/yooome/golang/raw/main/21-k8s%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B/Kubernetes%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B.md">Raw</a>
<a class="ui button edit-blame" href="/yooome/golang/blame/main/21-k8s%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B/Kubernetes%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B.md">Blame</a>
<a class="ui button edit-history" href="/yooome/golang/commits/main/21-k8s%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B/Kubernetes%E8%AF%A6%E7%BB%86%E6%95%99%E7%A8%8B.md">History</a>
</div>
<script>
  window.gon.aiCodeParams = {
    // pathWithNamespace: `yooome/golang`,
    // fileName: `21-k8s详细教程/Kubernetes详细教程.md`,
    // id: `b4ca8b8f1c0c6fb4f5fa8c2536a43b90e000944c`,
    // timeStamp: `1749598464`,
    // sign: `BrHT/dM0nR0pCs1rzka1XfSfFRqq9Xlpe2cZZ62KzpzxCRdu7wmNYfvj2anAp0BQwwWO+oRsqF5TMT2B9s1XV+ZDfNtgIvCyib9qcJrHG2s17dck5aR2GqN3wF9lNbMLFGRlyePr4sjINuJKihlcUA==`,
    blob:  $("#blob_raw").val(),
    type: "code",
    user: ``,
  }
  
  window.gon.blobName = `"Kubernetes详细教程.md"`
  $('.js-code-parsing').dropdown({
    on: 'hover',
    action: 'hide',
    onHide: function () {
    },
    onShow: function () {
    }
  });
  $(".ai-code-dropdown-box").find('.item').on("click", function (e) {
    window.jqxhr && window.jqxhr.abort();
    window.aiLoadingTimer && clearTimeout(window.aiLoadingTimer);
    aiReqLoading = false
  
    window.Gitee.setFullscreen(true);
    $(".side-toolbar").hide();
    var $siteContent = $(".site-content");
    // 获取最小高度
    var minHeight = parseInt($siteContent.css("min-height"));
    // 获取当前高度
    var currentHeight = parseInt($siteContent.height());
    if (minHeight + 1 > currentHeight) {
      $("#code-parsing").css("height", currentHeight);
    }
  
    $("#git-project-container").addClass('git-transition-width');
    $("#project-wrapper").css("marginTop", "-24px");
    //$("#git-project-container").removeClass("sixteen wide column");
    //$("#git-project-container").addClass("twelve wide column");
    if(!$("#code-parsing").hasClass("code-parsing-box")){
      $("#git-project-container").attr("style", "width: 75% !important;");
      $('.git-project-content-wrapper').find('#sixteen').attr("style", "width: 75% !important;");
      $('.right-wrapper').attr("style", "width: 75% !important;");
      $('.project-conter-container').attr("style", "width: 75% !important;");
    }
    $("#git-footer-main").css("margin-top", "14px");
    $("#code-parsing").addClass("code-parsing-box");
    // 当详情页宽度不够存放文件树时候隐藏
    var containerWidth = $("#project-wrapper").width();
    if (containerWidth < 1450) {
      $('.project-left-side-contaner').hide();
      $('#file-iconify-wrapper').removeClass('hide')
    }
  
    $(".code-parsing-content").hide();
    $(".skeleton").show();
    $(".ai_code_btns_simple").hide();
  
    $("#code-parsing").find(".markdown-body").innerHTML='';
  
    aiCodeType = $(this).data("value");
    aiSubTitle = $(this).data("text");
    handleAiReqInit()
  });
</script>
<script>
  "use strict";
  try {
    if((gon.wait_fork!=undefined && gon.wait_fork==true) || (gon.wait_fetch!=undefined && gon.wait_fetch==true)){
      $('.edit-blob').popup({content:"This repository is doing something background, pleace try again later", on: 'hover', delay: { show: 200, hide: 200 }});
      $('.edit-blob').click(function(e){
        e.preventDefault();
      })
    }
  
    var setUrl = function() {
      var params = window.location.search
      if (params==undefined || $.trim(params).length==0) return;
      $('span.options').children('.basic').find('a').each(function(index,ele){
        var origin_href = $(ele).attr('href');
        if (origin_href!="#" && origin_href.indexOf('?') == -1){
          $(ele).attr('href',origin_href+params);
        }
      });
    }
  
    setUrl();
  
    var clipboard = null,
        $btncopy  = $("#copy-text");
  
    clipboard = new Clipboard("#copy-text", {
      text: function(trigger) {
        return $("#blob_raw").val();
      }
    })
  
    clipboard.on('success', function(e) {
      $btncopy.popup('hide');
      $btncopy.popup('destroy');
      $btncopy.popup({content: 'Copied', position: 'bottom center'});
      $btncopy.popup('show');
    })
  
    clipboard.on('error', function(e) {
      var giteeModal = new GiteeModalHelper({okText: 'Confirm'});
      giteeModal.alert("Copy", 'Copy failed. Please copy it manually');
    })
  
    $(function() {
      $btncopy.popup({
        content: 'Copy to clipboard',
        position: 'bottom center'
      })
    })
  
  } catch (error) {
    console.log('blob/action error:' + error);
  }
  
  $(".disabled-edit-readonly").popup({
    content: "Readonly file is not editable",
    className: {
      popup: "ui popup",
    },
    position: "bottom center",
  });
  $(".disabled-edit-readonly, .disabled-edit-status").click(function () {
    return false;
  });
  $(".has_tooltip").popup({
    position: "top center",
  });
</script>
<style>
  .disabled-edit-readonly, .disabled-edit-status {
    background-color: #dcddde !important;
    color: rgba(0, 0, 0, 0.4) !important;
    opacity: 0.3 !important;
    background-image: none !important;
    -webkit-box-shadow: none !important;
            box-shadow: none !important;
    cursor: default !important; }
  
  .drawio-iframe-code-card {
    position: relative; }
    .drawio-iframe-code-card textarea {
      width: 100%;
      height: 140px;
      resize: none; }
    .drawio-iframe-code-card .icon-clone {
      position: absolute;
      right: 32px;
      bottom: 32px; }
    .drawio-iframe-code-card iframe {
      border-radius: 2px;
      border: 1px solid #DEDEDF; }
</style>
</div>
</div>
<div class='blob-header-title mt-1 ubblock_tip'>
</div>
<div class='contributor-description'><span class='recent-commit' style='margin-top: 0.7rem'>
<a class="commit-author-link  js-popover-card " data-username="yooome" href="/yooome">yooome</a>
<span>authored</span>
<span class='timeago commit-date' title='2023-08-03 01:03 +08:00'>
2023-08-03 01:03 +08:00
</span>
.
<a href="/yooome/golang/commit/bc577263c2182ccc18ba1dc8683460e5208d5f94">修改order</a>
</span>
</div>
</div>
<div class='clearfix'></div>
<div class='file_catalog'>
<div class='toggle'>
<i class='icon angle left'></i>
</div>
<div class='scroll-container'>
<div class='container'>
<div class='skeleton'>
<div class='line line1'></div>
<div class='line line2'></div>
<div class='line line3'></div>
<div class='line line1'></div>
<div class='line line2'></div>
<div class='line line3'></div>
</div>
</div>
</div>
</div>
<div class='file_content markdown-body'>
<blob-markdown-renderer data-dir='21-k8s详细教程' data-path-with-namespace='/yooome/golang'>&#x000A;<textarea class='content' style='display:none;'>## 							Kubernetes详细教程&#x000A;&#x000A;### 1. Kubernetes介绍&#x000A;&#x000A;#### 1.1 应用部署方式演变&#x000A;&#x000A;在部署应用程序的方式上，主要经历了三个时代：&#x000A;&#x000A;- **传统部署**：互联网早期，会直接将应用程序部署在物理机上&#x000A;&#x000A;  &gt; 优点：简单，不需要其它技术的参与&#x000A;  &gt;&#x000A;  &gt; 缺点：不能为应用程序定义资源使用边界，很难合理地分配计算资源，而且程序之间容易产生影响&#x000A;&#x000A;- **虚拟化部署**：可以在一台物理机上运行多个虚拟机，每个虚拟机都是独立的一个环境&#x000A;&#x000A;  &gt; 优点：程序环境不会相互产生影响，提供了一定程度的安全性&#x000A;  &gt;&#x000A;  &gt; 缺点：增加了操作系统，浪费了部分资源&#x000A;&#x000A;- **容器化部署**：与虚拟化类似，但是共享了操作系统&#x000A;&#x000A;  &gt; 优点：&#x000A;  &gt;&#x000A;  &gt; 可以保证每个容器拥有自己的文件系统、CPU、内存、进程空间等&#x000A;  &gt;&#x000A;  &gt; 运行应用程序所需要的资源都被容器包装，并和底层基础架构解耦&#x000A;  &gt;&#x000A;  &gt; 容器化的应用程序可以跨云服务商、跨Linux操作系统发行版进行部署&#x000A;&#x000A;![image-20200505183738289](./images/image-20200505183738289.png)&#x000A;&#x000A;容器化部署方式给带来很多的便利，但是也会出现一些问题，比如说：&#x000A;&#x000A;- 一个容器故障停机了，怎么样让另外一个容器立刻启动去替补停机的容器&#x000A;- 当并发访问量变大的时候，怎么样做到横向扩展容器数量&#x000A;&#x000A;这些容器管理的问题统称为**容器编排**问题，为了解决这些容器编排问题，就产生了一些容器编排的软件：&#x000A;&#x000A;- **Swarm**：Docker自己的容器编排工具&#x000A;- **Mesos**：Apache的一个资源统一管控的工具，需要和Marathon结合使用&#x000A;- **Kubernetes**：Google开源的的容器编排工具&#x000A;&#x000A;![image-20200524150339551](images/image-20200524150339551.png)&#x000A;&#x000A;#### 1.2 kubernetes简介&#x000A;&#x000A;![image-20200406232838722](./Kubenetes.assets/image-20200406232838722.png)&#x000A;&#x000A; &#x000A;&#x000A;kubernetes，是一个全新的基于容器技术的分布式架构领先方案，是谷歌严格保密十几年的秘密武器----Borg系统的一个开源版本，于2014年9月发布第一个版本，2015年7月发布第一个正式版本。&#x000A;&#x000A;kubernetes的本质是**一组服务器集群**，它可以在集群的每个节点上运行特定的程序，来对节点中的容器进行管理。目的是实现资源管理的自动化，主要提供了如下的主要功能：&#x000A;&#x000A;- **自我修复**：一旦某一个容器崩溃，能够在1秒中左右迅速启动新的容器&#x000A;- **弹性伸缩**：可以根据需要，自动对集群中正在运行的容器数量进行调整&#x000A;- **服务发现**：服务可以通过自动发现的形式找到它所依赖的服务&#x000A;- **负载均衡**：如果一个服务起动了多个容器，能够自动实现请求的负载均衡&#x000A;- **版本回退**：如果发现新发布的程序版本有问题，可以立即回退到原来的版本&#x000A;- **存储编排**：可以根据容器自身的需求自动创建存储卷&#x000A;&#x000A;#### 1.3 kubernetes组件&#x000A;&#x000A;一个kubernetes集群主要是由**控制节点(master)**、**工作节点(node)**构成，每个节点上都会安装不同的组件。&#x000A;&#x000A;**master：集群的控制平面，负责集群的决策 ( 管理 )**&#x000A;&#x000A;&gt; **ApiServer** : 资源操作的唯一入口，接收用户输入的命令，提供认证、授权、API注册和发现等机制&#x000A;&gt;&#x000A;&gt; **Scheduler** : 负责集群资源调度，按照预定的调度策略将Pod调度到相应的node节点上&#x000A;&gt;&#x000A;&gt; **ControllerManager** : 负责维护集群的状态，比如程序部署安排、故障检测、自动扩展、滚动更新等&#x000A;&gt;&#x000A;&gt; **Etcd** ：负责存储集群中各种资源对象的信息&#x000A;&#x000A;**node：集群的数据平面，负责为容器提供运行环境 ( 干活 )**&#x000A;&#x000A;&gt; **Kubelet** : 负责维护容器的生命周期，即通过控制docker，来创建、更新、销毁容器&#x000A;&gt;&#x000A;&gt; **KubeProxy** : 负责提供集群内部的服务发现和负载均衡&#x000A;&gt;&#x000A;&gt; **Docker** : 负责节点上容器的各种操作&#x000A;&#x000A;![image-20200406184656917](images/image-20200406184656917.png)&#x000A;&#x000A;下面，以部署一个nginx服务来说明kubernetes系统各个组件调用关系：&#x000A;&#x000A;1. 首先要明确，一旦kubernetes环境启动之后，master和node都会将自身的信息存储到etcd数据库中&#x000A;&#x000A;2. 一个nginx服务的安装请求会首先被发送到master节点的apiServer组件&#x000A;&#x000A;3. apiServer组件会调用scheduler组件来决定到底应该把这个服务安装到哪个node节点上&#x000A;&#x000A;   在此时，它会从etcd中读取各个node节点的信息，然后按照一定的算法进行选择，并将结果告知apiServer&#x000A;&#x000A;4. apiServer调用controller-manager去调度Node节点安装nginx服务&#x000A;&#x000A;5. kubelet接收到指令后，会通知docker，然后由docker来启动一个nginx的pod&#x000A;&#x000A;   pod是kubernetes的最小操作单元，容器必须跑在pod中至此，&#x000A;&#x000A;6. 一个nginx服务就运行了，如果需要访问nginx，就需要通过kube-proxy来对pod产生访问的代理&#x000A;&#x000A;这样，外界用户就可以访问集群中的nginx服务了&#x000A;&#x000A;#### 1.4 kubernetes概念&#x000A;&#x000A;**Master**：集群控制节点，每个集群需要至少一个master节点负责集群的管控&#x000A;&#x000A;**Node**：工作负载节点，由master分配容器到这些node工作节点上，然后node节点上的docker负责容器的运行&#x000A;&#x000A;**Pod**：kubernetes的最小控制单元，容器都是运行在pod中的，一个pod中可以有1个或者多个容器&#x000A;&#x000A;**Controller**：控制器，通过它来实现对pod的管理，比如启动pod、停止pod、伸缩pod的数量等等&#x000A;&#x000A;**Service**：pod对外服务的统一入口，下面可以维护者同一类的多个pod&#x000A;&#x000A;**Label**：标签，用于对pod进行分类，同一类pod会拥有相同的标签&#x000A;&#x000A;**NameSpace**：命名空间，用来隔离pod的运行环境&#x000A;&#x000A;### 2. kubernetes集群环境搭建&#x000A;&#x000A;#### 2.1 前置知识点&#x000A;&#x000A;目前生产部署Kubernetes 集群主要有两种方式：&#x000A;&#x000A;**kubeadm**&#x000A;&#x000A;Kubeadm 是一个K8s 部署工具，提供kubeadm init 和kubeadm join，用于快速部署Kubernetes 集群。&#x000A;&#x000A;官方地址：https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm/&#x000A;&#x000A;**二进制包**&#x000A;&#x000A;从github 下载发行版的二进制包，手动部署每个组件，组成Kubernetes 集群。&#x000A;&#x000A;Kubeadm 降低部署门槛，但屏蔽了很多细节，遇到问题很难排查。如果想更容易可控，推荐使用二进制包部署Kubernetes 集群，虽然手动部署麻烦点，期间可以学习很多工作原理，也利于后期维护。&#x000A;&#x000A;![image-20200404094800622](images/image-20200404094800622.png)&#x000A;&#x000A;#### 2.2 kubeadm 部署方式介绍&#x000A;&#x000A;kubeadm 是官方社区推出的一个用于快速部署kubernetes 集群的工具，这个工具能通过两条指令完成一个kubernetes 集群的部署：&#x000A;&#x000A;- 创建一个Master 节点kubeadm init&#x000A;- 将Node 节点加入到当前集群中$ kubeadm join &lt;Master 节点的IP 和端口&gt;&#x000A;&#x000A;#### 2.3 安装要求&#x000A;&#x000A;在开始之前，部署Kubernetes 集群机器需要满足以下几个条件：&#x000A;&#x000A;- 一台或多台机器，操作系统CentOS7.x-86_x64&#x000A;- 硬件配置：2GB 或更多RAM，2 个CPU 或更多CPU，硬盘30GB 或更多&#x000A;- 集群中所有机器之间网络互通&#x000A;- 可以访问外网，需要拉取镜像&#x000A;- 禁止swap 分区&#x000A;&#x000A;#### 2.4 最终目标&#x000A;&#x000A;- 在所有节点上安装Docker 和kubeadm&#x000A;- 部署Kubernetes Master&#x000A;- 部署容器网络插件&#x000A;- 部署Kubernetes Node，将节点加入Kubernetes 集群中&#x000A;- 部署Dashboard Web 页面，可视化查看Kubernetes 资源&#x000A;&#x000A;#### 2.5 准备环境 &#x000A;&#x000A;![image-20210609000002940](images/image-20210609000002940.png)&#x000A;&#x000A;| 角色     | IP地址      | 组件                              |&#x000A;| :------- | :---------- | :-------------------------------- |&#x000A;| master01 | 192.168.5.3 | docker，kubectl，kubeadm，kubelet |&#x000A;| node01   | 192.168.5.4 | docker，kubectl，kubeadm，kubelet |&#x000A;| node02   | 192.168.5.5 | docker，kubectl，kubeadm，kubelet |&#x000A;&#x000A;#### 2.6 环境初始化&#x000A;&#x000A;##### 2.6.1 检查操作系统的版本&#x000A;&#x000A;```powershell&#x000A;# 此方式下安装kubernetes集群要求Centos版本要在7.5或之上&#x000A;[root@master ~]# cat /etc/redhat-release&#x000A;Centos Linux 7.5.1804 (Core)&#x000A;```&#x000A;&#x000A;##### 2.6.2 主机名解析&#x000A;&#x000A;为了方便集群节点间的直接调用，在这个配置一下主机名解析，企业中推荐使用内部DNS服务器&#x000A;&#x000A;```powershell&#x000A;# 主机名成解析 编辑三台服务器的/etc/hosts文件，添加下面内容&#x000A;192.168.90.100 master&#x000A;192.168.90.106 node1&#x000A;192.168.90.107 node2&#x000A;```&#x000A;&#x000A;##### 2.6.3 时间同步&#x000A;&#x000A;kubernetes要求集群中的节点时间必须精确一直，这里使用chronyd服务从网络同步时间&#x000A;&#x000A;企业中建议配置内部的会见同步服务器&#x000A;&#x000A;```powershell&#x000A;# 启动chronyd服务&#x000A;[root@master ~]# systemctl start chronyd&#x000A;[root@master ~]# systemctl enable chronyd&#x000A;[root@master ~]# date&#x000A;```&#x000A;&#x000A;##### 2.6.4  禁用iptable和firewalld服务&#x000A;&#x000A;kubernetes和docker 在运行的中会产生大量的iptables规则，为了不让系统规则跟它们混淆，直接关闭系统的规则&#x000A;&#x000A;```powershell&#x000A;# 1 关闭firewalld服务&#x000A;[root@master ~]# systemctl stop firewalld&#x000A;[root@master ~]# systemctl disable firewalld&#x000A;# 2 关闭iptables服务&#x000A;[root@master ~]# systemctl stop iptables&#x000A;[root@master ~]# systemctl disable iptables&#x000A;```&#x000A;&#x000A;##### 2.6.5 禁用selinux&#x000A;&#x000A;selinux是linux系统下的一个安全服务，如果不关闭它，在安装集群中会产生各种各样的奇葩问题&#x000A;&#x000A;```powershell&#x000A;# 编辑 /etc/selinux/config 文件，修改SELINUX的值为disable&#x000A;# 注意修改完毕之后需要重启linux服务&#x000A;SELINUX=disabled&#x000A;```&#x000A;&#x000A;##### 2.6.6 禁用swap分区&#x000A;&#x000A;swap分区指的是虚拟内存分区，它的作用是物理内存使用完，之后将磁盘空间虚拟成内存来使用，启用swap设备会对系统的性能产生非常负面的影响，因此kubernetes要求每个节点都要禁用swap设备，但是如果因为某些原因确实不能关闭swap分区，就需要在集群安装过程中通过明确的参数进行配置说明&#x000A;&#x000A;```powershell&#x000A;# 编辑分区配置文件/etc/fstab，注释掉swap分区一行&#x000A;# 注意修改完毕之后需要重启linux服务&#x000A;vim /etc/fstab&#x000A;注释掉 /dev/mapper/centos-swap swap&#x000A;# /dev/mapper/centos-swap swap&#x000A;```&#x000A;&#x000A;##### 2.6.7 修改linux的内核参数&#x000A;&#x000A;```powershell&#x000A;# 修改linux的内核采纳数，添加网桥过滤和地址转发功能&#x000A;# 编辑/etc/sysctl.d/kubernetes.conf文件，添加如下配置：&#x000A;net.bridge.bridge-nf-call-ip6tables = 1&#x000A;net.bridge.bridge-nf-call-iptables = 1&#x000A;net.ipv4.ip_forward = 1&#x000A;&#x000A;# 重新加载配置&#x000A;[root@master ~]# sysctl -p&#x000A;# 加载网桥过滤模块&#x000A;[root@master ~]# modprobe br_netfilter&#x000A;# 查看网桥过滤模块是否加载成功&#x000A;[root@master ~]# lsmod | grep br_netfilter&#x000A;```&#x000A;&#x000A;##### 2.6.8 配置ipvs功能&#x000A;&#x000A;在Kubernetes中Service有两种带来模型，一种是基于iptables的，一种是基于ipvs的两者比较的话，ipvs的性能明显要高一些，但是如果要使用它，需要手动载入ipvs模块&#x000A;&#x000A;```powershell&#x000A;# 1.安装ipset和ipvsadm&#x000A;[root@master ~]# yum install ipset ipvsadm -y&#x000A;# 2.添加需要加载的模块写入脚本文件&#x000A;[root@master ~]# cat &lt;&lt;EOF&gt; /etc/sysconfig/modules/ipvs.modules&#x000A;#!/bin/bash&#x000A;modprobe -- ip_vs&#x000A;modprobe -- ip_vs_rr&#x000A;modprobe -- ip_vs_wrr&#x000A;modprobe -- ip_vs_sh&#x000A;modprobe -- nf_conntrack_ipv4&#x000A;EOF&#x000A;# 3.为脚本添加执行权限&#x000A;[root@master ~]# chmod +x /etc/sysconfig/modules/ipvs.modules&#x000A;# 4.执行脚本文件&#x000A;[root@master ~]# /bin/bash /etc/sysconfig/modules/ipvs.modules&#x000A;# 5.查看对应的模块是否加载成功&#x000A;[root@master ~]# lsmod | grep -e ip_vs -e nf_conntrack_ipv4&#x000A;```&#x000A;&#x000A;##### 2.6.9 安装docker&#x000A;&#x000A;```powershell&#x000A;# 1、切换镜像源&#x000A;[root@master ~]# wget https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo -O /etc/yum.repos.d/docker-ce.repo&#x000A;&#x000A;# 2、查看当前镜像源中支持的docker版本&#x000A;[root@master ~]# yum list docker-ce --showduplicates&#x000A;&#x000A;# 3、安装特定版本的docker-ce&#x000A;# 必须制定--setopt=obsoletes=0，否则yum会自动安装更高版本&#x000A;[root@master ~]# yum install --setopt=obsoletes=0 docker-ce-18.06.3.ce-3.el7 -y&#x000A;&#x000A;# 4、添加一个配置文件&#x000A;#Docker 在默认情况下使用Vgroup Driver为cgroupfs，而Kubernetes推荐使用systemd来替代cgroupfs&#x000A;[root@master ~]# mkdir /etc/docker&#x000A;[root@master ~]# cat &lt;&lt;EOF&gt; /etc/docker/daemon.json&#x000A;{&#x000A;	&quot;exec-opts&quot;: [&quot;native.cgroupdriver=systemd&quot;],&#x000A;	&quot;registry-mirrors&quot;: [&quot;https://kn0t2bca.mirror.aliyuncs.com&quot;]&#x000A;}&#x000A;EOF&#x000A;&#x000A;# 5、启动dokcer&#x000A;[root@master ~]# systemctl restart docker&#x000A;[root@master ~]# systemctl enable docker&#x000A;```&#x000A;&#x000A;##### 2.6.10 安装Kubernetes组件&#x000A;&#x000A;```powershell&#x000A;# 1、由于kubernetes的镜像在国外，速度比较慢，这里切换成国内的镜像源&#x000A;# 2、编辑/etc/yum.repos.d/kubernetes.repo,添加下面的配置&#x000A;[kubernetes]&#x000A;name=Kubernetes&#x000A;baseurl=http://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64&#x000A;enabled=1&#x000A;gpgchech=0&#x000A;repo_gpgcheck=0&#x000A;gpgkey=http://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg&#x000A;			http://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg&#x000A;&#x000A;# 3、安装kubeadm、kubelet和kubectl&#x000A;[root@master ~]# yum install --setopt=obsoletes=0 kubeadm-1.17.4-0 kubelet-1.17.4-0 kubectl-1.17.4-0 -y&#x000A;&#x000A;# 4、配置kubelet的cgroup&#x000A;#编辑/etc/sysconfig/kubelet, 添加下面的配置&#x000A;KUBELET_CGROUP_ARGS=&quot;--cgroup-driver=systemd&quot;&#x000A;KUBE_PROXY_MODE=&quot;ipvs&quot;&#x000A;&#x000A;# 5、设置kubelet开机自启&#x000A;[root@master ~]# systemctl enable kubelet&#x000A;```&#x000A;&#x000A;##### 2.6.11 准备集群镜像&#x000A;&#x000A;```powershell&#x000A;# 在安装kubernetes集群之前，必须要提前准备好集群需要的镜像，所需镜像可以通过下面命令查看&#x000A;[root@master ~]# kubeadm config images list&#x000A;&#x000A;# 下载镜像&#x000A;# 此镜像kubernetes的仓库中，由于网络原因，无法连接，下面提供了一种替换方案&#x000A;images=(&#x000A;	kube-apiserver:v1.17.4&#x000A;	kube-controller-manager:v1.17.4&#x000A;	kube-scheduler:v1.17.4&#x000A;	kube-proxy:v1.17.4&#x000A;	pause:3.1&#x000A;	etcd:3.4.3-0&#x000A;	coredns:1.6.5&#x000A;)&#x000A;&#x000A;for imageName in ${images[@]};do&#x000A;	docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/$imageName&#x000A;	docker tag registry.cn-hangzhou.aliyuncs.com/google_containers/$imageName k8s.gcr.io/$imageName&#x000A;	docker rmi registry.cn-hangzhou.aliyuncs.com/google_containers/$imageName &#x000A;done&#x000A;&#x000A;```&#x000A;&#x000A;##### 2.6.11 集群初始化&#x000A;&#x000A;&gt;下面的操作只需要在master节点上执行即可&#x000A;&#x000A;```powershell&#x000A;# 创建集群&#x000A;[root@master ~]# kubeadm init \&#x000A;	--apiserver-advertise-address=192.168.90.100 \&#x000A;	--image-repository registry.aliyuncs.com/google_containers \&#x000A;	--kubernetes-version=v1.17.4 \&#x000A;	--service-cidr=10.96.0.0/12 \&#x000A;	--pod-network-cidr=10.244.0.0/16&#x000A;# 创建必要文件&#x000A;[root@master ~]# mkdir -p $HOME/.kube&#x000A;[root@master ~]# sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config&#x000A;[root@master ~]# sudo chown $(id -u):$(id -g) $HOME/.kube/config&#x000A;```&#x000A;&#x000A;&gt; 下面的操作只需要在node节点上执行即可&#x000A;&#x000A;```powershell&#x000A;kubeadm join 192.168.0.100:6443 --token awk15p.t6bamck54w69u4s8 \&#x000A;    --discovery-token-ca-cert-hash sha256:a94fa09562466d32d29523ab6cff122186f1127599fa4dcd5fa0152694f17117 &#x000A;```&#x000A;&#x000A;在master上查看节点信息&#x000A;&#x000A;```powershell&#x000A;[root@master ~]# kubectl get nodes&#x000A;NAME    STATUS   ROLES     AGE   VERSION&#x000A;master  NotReady  master   6m    v1.17.4&#x000A;node1   NotReady   &lt;none&gt;  22s   v1.17.4&#x000A;node2   NotReady   &lt;none&gt;  19s   v1.17.4&#x000A;```&#x000A;&#x000A;##### 2.6.13 安装网络插件，只在master节点操作即可&#x000A;&#x000A;```powershell&#x000A;wget https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml&#x000A;```&#x000A;&#x000A;由于外网不好访问，如果出现无法访问的情况，可以直接用下面的 记得文件名是kube-flannel.yml，位置：/root/kube-flannel.yml内容：&#x000A;&#x000A;```powershell&#x000A;https://github.com/flannel-io/flannel/tree/master/Documentation/kube-flannel.yml&#x000A;```&#x000A;也可手动拉取指定版本&#x000A;docker pull quay.io/coreos/flannel:v0.14.0              #拉取flannel网络，三台主机&#x000A;docker images                  #查看仓库是否拉去下来&#x000A;&#x000A;```个人笔记```&#x000A;若是集群状态一直是 notready,用下面语句查看原因，&#x000A;journalctl -f -u kubelet.service&#x000A;若原因是： cni.go:237] Unable to update cni config: no networks found in /etc/cni/net.d&#x000A;mkdir -p /etc/cni/net.d                    #创建目录给flannel做配置文件&#x000A;vim /etc/cni/net.d/10-flannel.conf         #编写配置文件&#x000A;```powershell&#x000A;&#x000A;{&#x000A; &quot;name&quot;:&quot;cbr0&quot;,&#x000A; &quot;cniVersion&quot;:&quot;0.3.1&quot;,&#x000A; &quot;type&quot;:&quot;flannel&quot;,&#x000A; &quot;deledate&quot;:{&#x000A;    &quot;hairpinMode&quot;:true,&#x000A;    &quot;isDefaultGateway&quot;:true&#x000A;  }&#x000A;&#x000A;}&#x000A;&#x000A;```&#x000A;&#x000A;&#x000A;##### 2.6.14 使用kubeadm reset重置集群&#x000A;&#x000A;```&#x000A;#在master节点之外的节点进行操作&#x000A;kubeadm reset&#x000A;systemctl stop kubelet&#x000A;systemctl stop docker&#x000A;rm -rf /var/lib/cni/&#x000A;rm -rf /var/lib/kubelet/*&#x000A;rm -rf /etc/cni/&#x000A;ifconfig cni0 down&#x000A;ifconfig flannel.1 down&#x000A;ifconfig docker0 down&#x000A;ip link delete cni0&#x000A;ip link delete flannel.1&#x000A;##重启kubelet&#x000A;systemctl restart kubelet&#x000A;##重启docker&#x000A;systemctl restart docker&#x000A;```&#x000A;&#x000A;##### 2.6.15 重启kubelet和docker&#x000A;&#x000A;```powershell&#x000A;# 重启kubelet&#x000A;systemctl restart kubelet&#x000A;# 重启docker&#x000A;systemctl restart docker&#x000A;```&#x000A;&#x000A;使用配置文件启动fannel&#x000A;&#x000A;```powershell&#x000A;kubectl apply -f kube-flannel.yml&#x000A;```&#x000A;&#x000A;等待它安装完毕 发现已经是 集群的状态已经是Ready&#x000A;&#x000A;![img](images/2232696-20210621233106024-1676033717.png)&#x000A;&#x000A;##### 2.6.16 kubeadm中的命令&#x000A;&#x000A;```powershell&#x000A;# 生成 新的token&#x000A;[root@master ~]# kubeadm token create --print-join-command&#x000A;```&#x000A;&#x000A;#### 2.7 集群测试&#x000A;&#x000A;##### 2.7.1 创建一个nginx服务&#x000A;&#x000A;```powershell&#x000A;kubectl create deployment nginx  --image=nginx:1.14-alpine&#x000A;```&#x000A;&#x000A;##### 2.7.2 暴露端口&#x000A;&#x000A;```powershell&#x000A;kubectl expose deploy nginx  --port=80 --target-port=80  --type=NodePort&#x000A;```&#x000A;&#x000A;##### 2.7.3 查看服务&#x000A;&#x000A;```powershell&#x000A;kubectl get pod,svc&#x000A;```&#x000A;&#x000A;##### 2.7.4 查看pod&#x000A;&#x000A;![2232696-20210621233130477-111035427](images/2232696-20210621233130477-111035427.png)&#x000A;&#x000A;浏览器测试结果：&#x000A;&#x000A;![img](images/2232696-20210621233157075-1117518703.png)&#x000A;&#x000A;### 3. 资源管理&#x000A;&#x000A;#### 3.1 资源管理介绍&#x000A;&#x000A;在kubernetes中，所有的内容都抽象为资源，用户需要通过操作资源来管理kubernetes。&#x000A;&#x000A;&gt; kubernetes的本质上就是一个集群系统，用户可以在集群中部署各种服务，所谓的部署服务，其实就是在kubernetes集群中运行一个个的容器，并将指定的程序跑在容器中。&#x000A;&gt;&#x000A;&gt; kubernetes的最小管理单元是pod而不是容器，所以只能将容器放在`Pod`中，而kubernetes一般也不会直接管理Pod，而是通过`Pod控制器`来管理Pod的。&#x000A;&gt;&#x000A;&gt; Pod可以提供服务之后，就要考虑如何访问Pod中服务，kubernetes提供了`Service`资源实现这个功能。&#x000A;&gt;&#x000A;&gt; 当然，如果Pod中程序的数据需要持久化，kubernetes还提供了各种`存储`系统。&#x000A;&#x000A;![image-20200406225334627](Kubenetes.assets/image-20200406225334627.png)&#x000A;&#x000A;&gt; 学习kubernetes的核心，就是学习如何对集群上的`Pod、Pod控制器、Service、存储`等各种资源进行操作&#x000A;&#x000A;#### 3.2 YAML语言介绍&#x000A;&#x000A;YAML是一个类似 XML、JSON 的标记性语言。它强调以**数据**为中心，并不是以标识语言为重点。因而YAML本身的定义比较简单，号称&quot;一种人性化的数据格式语言&quot;。&#x000A;&#x000A;```&#x000A;&lt;heima&gt;&#x000A;    &lt;age&gt;15&lt;/age&gt;&#x000A;    &lt;address&gt;Beijing&lt;/address&gt;&#x000A;&lt;/heima&gt;&#x000A;```&#x000A;&#x000A;```&#x000A;heima:&#x000A;  age: 15&#x000A;  address: Beijing&#x000A;```&#x000A;&#x000A;YAML的语法比较简单，主要有下面几个：&#x000A;&#x000A;- 大小写敏感&#x000A;- 使用缩进表示层级关系&#x000A;- 缩进不允许使用tab，只允许空格( 低版本限制 )&#x000A;- 缩进的空格数不重要，只要相同层级的元素左对齐即可&#x000A;- '#'表示注释&#x000A;&#x000A;YAML支持以下几种数据类型：&#x000A;&#x000A;- 纯量：单个的、不可再分的值&#x000A;- 对象：键值对的集合，又称为映射（mapping）/ 哈希（hash） / 字典（dictionary）&#x000A;- 数组：一组按次序排列的值，又称为序列（sequence） / 列表（list）&#x000A;&#x000A;```yml&#x000A;# 纯量, 就是指的一个简单的值，字符串、布尔值、整数、浮点数、Null、时间、日期&#x000A;# 1 布尔类型&#x000A;c1: true (或者True)&#x000A;# 2 整型&#x000A;c2: 234&#x000A;# 3 浮点型&#x000A;c3: 3.14&#x000A;# 4 null类型 &#x000A;c4: ~  # 使用~表示null&#x000A;# 5 日期类型&#x000A;c5: 2018-02-17    # 日期必须使用ISO 8601格式，即yyyy-MM-dd&#x000A;# 6 时间类型&#x000A;c6: 2018-02-17T15:02:31+08:00  # 时间使用ISO 8601格式，时间和日期之间使用T连接，最后使用+代表时区&#x000A;# 7 字符串类型&#x000A;c7: heima     # 简单写法，直接写值 , 如果字符串中间有特殊字符，必须使用双引号或者单引号包裹 &#x000A;c8: line1&#x000A;    line2     # 字符串过多的情况可以拆成多行，每一行会被转化成一个空格&#x000A;```&#x000A;&#x000A;&#x000A;&#x000A;```yaml&#x000A;# 对象&#x000A;# 形式一(推荐):&#x000A;heima:&#x000A;  age: 15&#x000A;  address: Beijing&#x000A;# 形式二(了解):&#x000A;heima: {age: 15,address: Beijing}&#x000A;```&#x000A;&#x000A;```yaml&#x000A;# 数组&#x000A;# 形式一(推荐):&#x000A;address:&#x000A;  - 顺义&#x000A;  - 昌平  &#x000A;# 形式二(了解):&#x000A;address: [顺义,昌平]&#x000A;```&#x000A;&#x000A;&gt; 小提示：&#x000A;&gt;&#x000A;&gt; 1 书写yaml切记`:` 后面要加一个空格&#x000A;&gt;&#x000A;&gt; 2 如果需要将多段yaml配置放在一个文件中，中间要使用`---`分隔&#x000A;&gt;&#x000A;&gt; 3 下面是一个yaml转json的网站，可以通过它验证yaml是否书写正确&#x000A;&gt;&#x000A;&gt; https://www.json2yaml.com/convert-yaml-to-json&#x000A;&#x000A;#### 3.3 资源管理方式&#x000A;&#x000A;- 命令式对象管理：直接使用命令去操作kubernetes资源&#x000A;&#x000A;  ``` powershell&#x000A;  kubectl run nginx-pod --image=nginx:1.17.1 --port=80&#x000A;  ```&#x000A;&#x000A;- 命令式对象配置：通过命令配置和配置文件去操作kubernetes资源&#x000A;&#x000A;  ```powershell&#x000A;  kubectl create/patch -f nginx-pod.yaml&#x000A;  ```&#x000A;&#x000A;- 声明式对象配置：通过apply命令和配置文件去操作kubernetes资源&#x000A;&#x000A;  ```powershell&#x000A;  kubectl apply -f nginx-pod.yaml&#x000A;  ```&#x000A;  &#x000A;  &#x000A;&#x000A;| 类型           | 操作对象 | 适用环境 | 优点           | 缺点                             |&#x000A;| :------------- | :------- | :------- | :------------- | :------------------------------- |&#x000A;| 命令式对象管理 | 对象     | 测试     | 简单           | 只能操作活动对象，无法审计、跟踪 |&#x000A;| 命令式对象配置 | 文件     | 开发     | 可以审计、跟踪 | 项目大时，配置文件多，操作麻烦   |&#x000A;| 声明式对象配置 | 目录     | 开发     | 支持目录操作   | 意外情况下难以调试               |&#x000A;&#x000A;##### 3.3.1 命令式对象管理&#x000A;&#x000A;**kubectl命令**&#x000A;&#x000A;kubectl是kubernetes集群的命令行工具，通过它能够对集群本身进行管理，并能够在集群上进行容器化应用的安装部署。kubectl命令的语法如下：&#x000A;&#x000A;```&#x000A;kubectl [command] [type] [name] [flags]&#x000A;```&#x000A;&#x000A;**comand**：指定要对资源执行的操作，例如create、get、delete&#x000A;&#x000A;**type**：指定资源类型，比如deployment、pod、service&#x000A;&#x000A;**name**：指定资源的名称，名称大小写敏感&#x000A;&#x000A;**flags**：指定额外的可选参数&#x000A;&#x000A;```shell&#x000A;# 查看所有pod&#x000A;kubectl get pod &#x000A;&#x000A;# 查看某个pod&#x000A;kubectl get pod pod_name&#x000A;&#x000A;# 查看某个pod,以yaml格式展示结果&#x000A;kubectl get pod pod_name -o yaml&#x000A;```&#x000A;&#x000A;**资源类型**&#x000A;&#x000A;kubernetes中所有的内容都抽象为资源，可以通过下面的命令进行查看:&#x000A;&#x000A;```&#x000A;kubectl api-resources&#x000A;```&#x000A;&#x000A;经常使用的资源有下面这些：&#x000A;&#x000A;| 资源分类      | 资源名称                 | 缩写    | 资源作用        |&#x000A;| :------------ | :----------------------- | :------ | :-------------- |&#x000A;| 集群级别资源  | nodes                    | no      | 集群组成部分    |&#x000A;| namespaces    | ns                       | 隔离Pod |                 |&#x000A;| pod资源       | pods                     | po      | 装载容器        |&#x000A;| pod资源控制器 | replicationcontrollers   | rc      | 控制pod资源     |&#x000A;|               | replicasets              | rs      | 控制pod资源     |&#x000A;|               | deployments              | deploy  | 控制pod资源     |&#x000A;|               | daemonsets               | ds      | 控制pod资源     |&#x000A;|               | jobs                     |         | 控制pod资源     |&#x000A;|               | cronjobs                 | cj      | 控制pod资源     |&#x000A;|               | horizontalpodautoscalers | hpa     | 控制pod资源     |&#x000A;|               | statefulsets             | sts     | 控制pod资源     |&#x000A;| 服务发现资源  | services                 | svc     | 统一pod对外接口 |&#x000A;|               | ingress                  | ing     | 统一pod对外接口 |&#x000A;| 存储资源      | volumeattachments        |         | 存储            |&#x000A;|               | persistentvolumes        | pv      | 存储            |&#x000A;|               | persistentvolumeclaims   | pvc     | 存储            |&#x000A;| 配置资源      | configmaps               | cm      | 配置            |&#x000A;|               | secrets                  |         | 配置            |&#x000A;&#x000A;**操作**&#x000A;&#x000A;kubernetes允许对资源进行多种操作，可以通过--help查看详细的操作命令&#x000A;&#x000A;```&#x000A;kubectl --help&#x000A;```&#x000A;&#x000A;经常使用的操作有下面这些：&#x000A;&#x000A;| 命令分类   | 命令         | 翻译                        | 命令作用                     |&#x000A;| :--------- | :----------- | :-------------------------- | :--------------------------- |&#x000A;| 基本命令   | create       | 创建                        | 创建一个资源                 |&#x000A;|            | edit         | 编辑                        | 编辑一个资源                 |&#x000A;|            | get          | 获取                        | 获取一个资源                 |&#x000A;|            | patch        | 更新                        | 更新一个资源                 |&#x000A;|            | delete       | 删除                        | 删除一个资源                 |&#x000A;|            | explain      | 解释                        | 展示资源文档                 |&#x000A;| 运行和调试 | run          | 运行                        | 在集群中运行一个指定的镜像   |&#x000A;|            | expose       | 暴露                        | 暴露资源为Service            |&#x000A;|            | describe     | 描述                        | 显示资源内部信息             |&#x000A;|            | logs         | 日志输出容器在 pod 中的日志 | 输出容器在 pod 中的日志      |&#x000A;|            | attach       | 缠绕进入运行中的容器        | 进入运行中的容器             |&#x000A;|            | exec         | 执行容器中的一个命令        | 执行容器中的一个命令         |&#x000A;|            | cp           | 复制                        | 在Pod内外复制文件            |&#x000A;|            | rollout      | 首次展示                    | 管理资源的发布               |&#x000A;|            | scale        | 规模                        | 扩(缩)容Pod的数量            |&#x000A;|            | autoscale    | 自动调整                    | 自动调整Pod的数量            |&#x000A;| 高级命令   | apply        | rc                          | 通过文件对资源进行配置       |&#x000A;|            | label        | 标签                        | 更新资源上的标签             |&#x000A;| 其他命令   | cluster-info | 集群信息                    | 显示集群信息                 |&#x000A;|            | version      | 版本                        | 显示当前Server和Client的版本 |&#x000A;&#x000A;下面以一个namespace / pod的创建和删除简单演示下命令的使用：&#x000A;&#x000A;```shell&#x000A;# 创建一个namespace&#x000A;[root@master ~]# kubectl create namespace dev&#x000A;namespace/dev created&#x000A;&#x000A;# 获取namespace&#x000A;[root@master ~]# kubectl get ns&#x000A;NAME              STATUS   AGE&#x000A;default           Active   21h&#x000A;dev               Active   21s&#x000A;kube-node-lease   Active   21h&#x000A;kube-public       Active   21h&#x000A;kube-system       Active   21h&#x000A;&#x000A;# 在此namespace下创建并运行一个nginx的Pod&#x000A;[root@master ~]# kubectl run pod --image=nginx:latest -n dev&#x000A;kubectl run --generator=deployment/apps.v1 is DEPRECATED and will be removed in a future version. Use kubectl run --generator=run-pod/v1 or kubectl create instead.&#x000A;deployment.apps/pod created&#x000A;&#x000A;# 查看新创建的pod&#x000A;[root@master ~]# kubectl get pod -n dev&#x000A;NAME  READY   STATUS    RESTARTS   AGE&#x000A;pod   1/1     Running   0          21s&#x000A;&#x000A;# 删除指定的pod&#x000A;[root@master ~]# kubectl delete pod pod-864f9875b9-pcw7x&#x000A;pod &quot;pod&quot; deleted&#x000A;&#x000A;# 删除指定的namespace&#x000A;[root@master ~]# kubectl delete ns dev&#x000A;namespace &quot;dev&quot; deleted&#x000A;```&#x000A;&#x000A;### 3.3.2 命令式对象配置&#x000A;&#x000A;命令式对象配置就是使用命令配合配置文件一起来操作kubernetes资源。&#x000A;&#x000A;1） 创建一个nginxpod.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Namespace&#x000A;metadata:&#x000A;  name: dev&#x000A;&#x000A;---&#x000A;&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: nginxpod&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx-containers&#x000A;    image: nginx:latest&#x000A;```&#x000A;&#x000A;2）执行create命令，创建资源：&#x000A;&#x000A;```powershell&#x000A;[root@master ~]# kubectl create -f nginxpod.yaml&#x000A;namespace/dev created&#x000A;pod/nginxpod created&#x000A;```&#x000A;&#x000A;此时发现创建了两个资源对象，分别是namespace和pod&#x000A;&#x000A;3）执行get命令，查看资源：&#x000A;&#x000A;```shell&#x000A;[root@master ~]#  kubectl get -f nginxpod.yaml&#x000A;NAME            STATUS   AGE&#x000A;namespace/dev   Active   18s&#x000A;&#x000A;NAME            READY   STATUS    RESTARTS   AGE&#x000A;pod/nginxpod    1/1     Running   0          17s&#x000A;```&#x000A;&#x000A;这样就显示了两个资源对象的信息&#x000A;&#x000A;4）执行delete命令，删除资源：&#x000A;&#x000A;```shell&#x000A;[root@master ~]# kubectl delete -f nginxpod.yaml&#x000A;namespace &quot;dev&quot; deleted&#x000A;pod &quot;nginxpod&quot; deleted&#x000A;```&#x000A;&#x000A;此时发现两个资源对象被删除了&#x000A;&#x000A;```&#x000A;总结:&#x000A;    命令式对象配置的方式操作资源，可以简单的认为：命令  +  yaml配置文件（里面是命令需要的各种参数）&#x000A;```&#x000A;&#x000A;### 3.3.3 声明式对象配置&#x000A;&#x000A;声明式对象配置跟命令式对象配置很相似，但是它只有一个命令apply。&#x000A;&#x000A;```shell&#x000A;# 首先执行一次kubectl apply -f yaml文件，发现创建了资源&#x000A;[root@master ~]#  kubectl apply -f nginxpod.yaml&#x000A;namespace/dev created&#x000A;pod/nginxpod created&#x000A;&#x000A;# 再次执行一次kubectl apply -f yaml文件，发现说资源没有变动&#x000A;[root@master ~]#  kubectl apply -f nginxpod.yaml&#x000A;namespace/dev unchanged&#x000A;pod/nginxpod unchanged&#x000A;```&#x000A;&#x000A;```powershell&#x000A;总结:&#x000A;    其实声明式对象配置就是使用apply描述一个资源最终的状态（在yaml中定义状态）&#x000A;    使用apply操作资源：&#x000A;        如果资源不存在，就创建，相当于 kubectl create&#x000A;        如果资源已存在，就更新，相当于 kubectl patch&#x000A;```&#x000A;&#x000A;&gt; 扩展：kubectl可以在node节点上运行吗 ?&#x000A;&#x000A;kubectl的运行是需要进行配置的，它的配置文件是$HOME/.kube，如果想要在node节点运行此命令，需要将master上的.kube文件复制到node节点上，即在master节点上执行下面操作：&#x000A;&#x000A;```shell&#x000A;scp  -r  HOME/.kube   node1: HOME/&#x000A;```&#x000A;&#x000A;&gt; 使用推荐: 三种方式应该怎么用 ?&#x000A;&#x000A;创建/更新资源 使用声明式对象配置 kubectl apply -f XXX.yaml&#x000A;&#x000A;删除资源 使用命令式对象配置 kubectl delete -f XXX.yaml&#x000A;&#x000A;查询资源 使用命令式对象管理 kubectl get(describe) 资源名称&#x000A;&#x000A;### 4. 实战入门&#x000A;&#x000A;本章节将介绍如何在kubernetes集群中部署一个nginx服务，并且能够对其进行访问。&#x000A;&#x000A;#### 4.1 Namespace&#x000A;&#x000A;Namespace是kubernetes系统中的一种非常重要资源，它的主要作用是用来实现**多套环境的资源隔离**或者**多租户的资源隔离**。&#x000A;&#x000A;默认情况下，kubernetes集群中的所有的Pod都是可以相互访问的。但是在实际中，可能不想让两个Pod之间进行互相的访问，那此时就可以将两个Pod划分到不同的namespace下。kubernetes通过将集群内部的资源分配到不同的Namespace中，可以形成逻辑上的&quot;组&quot;，以方便不同的组的资源进行隔离使用和管理。&#x000A;&#x000A;可以通过kubernetes的授权机制，将不同的namespace交给不同租户进行管理，这样就实现了多租户的资源隔离。此时还能结合kubernetes的资源配额机制，限定不同租户能占用的资源，例如CPU使用量、内存使用量等等，来实现租户可用资源的管理。&#x000A;&#x000A;![image-20200407100850484](Kubenetes.assets/image-20200407100850484.png)&#x000A;&#x000A;kubernetes在集群启动之后，会默认创建几个namespace&#x000A;&#x000A;&#x000A;&#x000A;```shell&#x000A;[root@master ~]# kubectl  get namespace&#x000A;NAME              STATUS   AGE&#x000A;default           Active   45h     #  所有未指定Namespace的对象都会被分配在default命名空间&#x000A;kube-node-lease   Active   45h     #  集群节点之间的心跳维护，v1.13开始引入&#x000A;kube-public       Active   45h     #  此命名空间下的资源可以被所有人访问（包括未认证用户）&#x000A;kube-system       Active   45h     #  所有由Kubernetes系统创建的资源都处于这个命名空间&#x000A;```&#x000A;&#x000A;下面来看namespace资源的具体操作：&#x000A;&#x000A;##### 4.1.1 **查看**&#x000A;&#x000A;```shell&#x000A;# 1 查看所有的ns  命令：kubectl get ns&#x000A;[root@master ~]# kubectl get ns&#x000A;NAME              STATUS   AGE&#x000A;default           Active   45h&#x000A;kube-node-lease   Active   45h&#x000A;kube-public       Active   45h     &#x000A;kube-system       Active   45h     &#x000A;&#x000A;# 2 查看指定的ns   命令：kubectl get ns ns名称&#x000A;[root@master ~]# kubectl get ns default&#x000A;NAME      STATUS   AGE&#x000A;default   Active   45h&#x000A;&#x000A;# 3 指定输出格式  命令：kubectl get ns ns名称  -o 格式参数&#x000A;# kubernetes支持的格式有很多，比较常见的是wide、json、yaml&#x000A;[root@master ~]# kubectl get ns default -o yaml&#x000A;apiVersion: v1&#x000A;kind: Namespace&#x000A;metadata:&#x000A;  creationTimestamp: &quot;2021-05-08T04:44:16Z&quot;&#x000A;  name: default&#x000A;  resourceVersion: &quot;151&quot;&#x000A;  selfLink: /api/v1/namespaces/default&#x000A;  uid: 7405f73a-e486-43d4-9db6-145f1409f090&#x000A;spec:&#x000A;  finalizers:&#x000A;  - kubernetes&#x000A;status:&#x000A;  phase: Active&#x000A;  &#x000A;# 4 查看ns详情  命令：kubectl describe ns ns名称&#x000A;[root@master ~]# kubectl describe ns default&#x000A;Name:         default&#x000A;Labels:       &lt;none&gt;&#x000A;Annotations:  &lt;none&gt;&#x000A;Status:       Active  # Active 命名空间正在使用中  Terminating 正在删除命名空间&#x000A;&#x000A;# ResourceQuota 针对namespace做的资源限制&#x000A;# LimitRange针对namespace中的每个组件做的资源限制&#x000A;No resource quota.&#x000A;No LimitRange resource.&#x000A;```&#x000A;&#x000A;##### 4.1.2 **创建**&#x000A;&#x000A;```shell&#x000A;# 创建namespace&#x000A;[root@master ~]# kubectl create ns dev&#x000A;namespace/dev created&#x000A;```&#x000A;&#x000A;##### 4.1.3 **删除**&#x000A;&#x000A;```shell&#x000A;# 删除namespace&#x000A;[root@master ~]# kubectl delete ns dev&#x000A;namespace &quot;dev&quot; deleted&#x000A;```&#x000A;&#x000A;##### 4.1.4 **配置方式**&#x000A;&#x000A;首先准备一个yaml文件：ns-dev.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Namespace&#x000A;metadata:&#x000A;  name: dev&#x000A;```&#x000A;&#x000A;然后就可以执行对应的创建和删除命令了：&#x000A;&#x000A;创建：kubectl create -f ns-dev.yaml&#x000A;&#x000A;删除：kubectl delete -f ns-dev.yaml&#x000A;&#x000A;#### 4.2 Pod&#x000A;&#x000A;Pod是kubernetes集群进行管理的最小单元，程序要运行必须部署在容器中，而容器必须存在于Pod中。&#x000A;&#x000A;Pod可以认为是容器的封装，一个Pod中可以存在一个或者多个容器。&#x000A;&#x000A;![image-20200407121501907](Kubenetes.assets/image-20200407121501907.png)&#x000A;&#x000A;kubernetes在集群启动之后，集群中的各个组件也都是以Pod方式运行的。可以通过下面命令查看：&#x000A;&#x000A;```shell&#x000A;[root@master ~]# kubectl get pod -n kube-system&#x000A;NAMESPACE     NAME                             READY   STATUS    RESTARTS   AGE&#x000A;kube-system   coredns-6955765f44-68g6v         1/1     Running   0          2d1h&#x000A;kube-system   coredns-6955765f44-cs5r8         1/1     Running   0          2d1h&#x000A;kube-system   etcd-master                      1/1     Running   0          2d1h&#x000A;kube-system   kube-apiserver-master            1/1     Running   0          2d1h&#x000A;kube-system   kube-controller-manager-master   1/1     Running   0          2d1h&#x000A;kube-system   kube-flannel-ds-amd64-47r25      1/1     Running   0          2d1h&#x000A;kube-system   kube-flannel-ds-amd64-ls5lh      1/1     Running   0          2d1h&#x000A;kube-system   kube-proxy-685tk                 1/1     Running   0          2d1h&#x000A;kube-system   kube-proxy-87spt                 1/1     Running   0          2d1h&#x000A;kube-system   kube-scheduler-master            1/1     Running   0          2d1h&#x000A;```&#x000A;&#x000A;##### 4.2.1 创建并运行&#x000A;&#x000A;kubernetes没有提供单独运行Pod的命令，都是通过Pod控制器来实现的&#x000A;&#x000A;```shell&#x000A;# 命令格式： kubectl run (pod控制器名称) [参数] &#x000A;# --image  指定Pod的镜像&#x000A;# --port   指定端口&#x000A;# --namespace  指定namespace&#x000A;[root@master ~]# kubectl run nginx --image=nginx:latest --port=80 --namespace dev &#x000A;deployment.apps/nginx created&#x000A;```&#x000A;&#x000A;##### 4.2.2 查看pod信息&#x000A;&#x000A;```shell&#x000A;# 查看Pod基本信息&#x000A;[root@master ~]# kubectl get pods -n dev&#x000A;NAME    READY   STATUS    RESTARTS   AGE&#x000A;nginx   1/1     Running   0          43s&#x000A;&#x000A;# 查看Pod的详细信息&#x000A;[root@master ~]# kubectl describe pod nginx -n dev&#x000A;Name:         nginx&#x000A;Namespace:    dev&#x000A;Priority:     0&#x000A;Node:         node1/192.168.5.4&#x000A;Start Time:   Wed, 08 May 2021 09:29:24 +0800&#x000A;Labels:       pod-template-hash=5ff7956ff6&#x000A;              run=nginx&#x000A;Annotations:  &lt;none&gt;&#x000A;Status:       Running&#x000A;IP:           10.244.1.23&#x000A;IPs:&#x000A;  IP:           10.244.1.23&#x000A;Controlled By:  ReplicaSet/nginx&#x000A;Containers:&#x000A;  nginx:&#x000A;    Container ID:   docker://4c62b8c0648d2512380f4ffa5da2c99d16e05634979973449c98e9b829f6253c&#x000A;    Image:          nginx:latest&#x000A;    Image ID:       docker-pullable://nginx@sha256:485b610fefec7ff6c463ced9623314a04ed67e3945b9c08d7e53a47f6d108dc7&#x000A;    Port:           80/TCP&#x000A;    Host Port:      0/TCP&#x000A;    State:          Running&#x000A;      Started:      Wed, 08 May 2021 09:30:01 +0800&#x000A;    Ready:          True&#x000A;    Restart Count:  0&#x000A;    Environment:    &lt;none&gt;&#x000A;    Mounts:&#x000A;      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hwvvw (ro)&#x000A;Conditions:&#x000A;  Type              Status&#x000A;  Initialized       True&#x000A;  Ready             True&#x000A;  ContainersReady   True&#x000A;  PodScheduled      True&#x000A;Volumes:&#x000A;  default-token-hwvvw:&#x000A;    Type:        Secret (a volume populated by a Secret)&#x000A;    SecretName:  default-token-hwvvw&#x000A;    Optional:    false&#x000A;QoS Class:       BestEffort&#x000A;Node-Selectors:  &lt;none&gt;&#x000A;Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s&#x000A;                 node.kubernetes.io/unreachable:NoExecute for 300s&#x000A;Events:&#x000A;  Type    Reason     Age        From               Message&#x000A;  ----    ------     ----       ----               -------&#x000A;  Normal  Scheduled  &lt;unknown&gt;  default-scheduler  Successfully assigned dev/nginx-5ff7956ff6-fg2db to node1&#x000A;  Normal  Pulling    4m11s      kubelet, node1     Pulling image &quot;nginx:latest&quot;&#x000A;  Normal  Pulled     3m36s      kubelet, node1     Successfully pulled image &quot;nginx:latest&quot;&#x000A;  Normal  Created    3m36s      kubelet, node1     Created container nginx&#x000A;  Normal  Started    3m36s      kubelet, node1     Started container nginx&#x000A;```&#x000A;&#x000A;##### 4.2.3 访问Pod&#x000A;&#x000A;```shell&#x000A;# 获取podIP&#x000A;[root@master ~]# kubectl get pods -n dev -o wide&#x000A;NAME    READY   STATUS    RESTARTS   AGE    IP             NODE    ... &#x000A;nginx   1/1     Running   0          190s   10.244.1.23   node1   ...&#x000A;&#x000A;#访问POD&#x000A;[root@master ~]# curl http://10.244.1.23:80&#x000A;&lt;!DOCTYPE html&gt;&#x000A;&lt;html&gt;&#x000A;&lt;head&gt;&#x000A;	&lt;title&gt;Welcome to nginx!&lt;/title&gt;&#x000A;&lt;/head&gt;&#x000A;&lt;body&gt;&#x000A;	&lt;p&gt;&lt;em&gt;Thank you for using nginx.&lt;/em&gt;&lt;/p&gt;&#x000A;&lt;/body&gt;&#x000A;&lt;/html&gt;&#x000A;```&#x000A;&#x000A;##### 4.2.4 删除指定Pod&#x000A;&#x000A;```shell&#x000A;# 删除指定Pod&#x000A;[root@master ~]# kubectl delete pod nginx -n dev&#x000A;pod &quot;nginx&quot; deleted&#x000A;&#x000A;# 此时，显示删除Pod成功，但是再查询，发现又新产生了一个 &#x000A;[root@master ~]# kubectl get pods -n dev&#x000A;NAME    READY   STATUS    RESTARTS   AGE&#x000A;nginx   1/1     Running   0          21s&#x000A;&#x000A;# 这是因为当前Pod是由Pod控制器创建的，控制器会监控Pod状况，一旦发现Pod死亡，会立即重建&#x000A;# 此时要想删除Pod，必须删除Pod控制器&#x000A;&#x000A;# 先来查询一下当前namespace下的Pod控制器&#x000A;[root@master ~]# kubectl get deploy -n  dev&#x000A;NAME    READY   UP-TO-DATE   AVAILABLE   AGE&#x000A;nginx   1/1     1            1           9m7s&#x000A;&#x000A;# 接下来，删除此PodPod控制器&#x000A;[root@master ~]# kubectl delete deploy nginx -n dev&#x000A;deployment.apps &quot;nginx&quot; deleted&#x000A;&#x000A;# 稍等片刻，再查询Pod，发现Pod被删除了&#x000A;[root@master ~]# kubectl get pods -n dev&#x000A;No resources found in dev namespace.&#x000A;```&#x000A;&#x000A;##### 4.2.5 配置操作&#x000A;&#x000A;创建一个pod-nginx.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: nginx&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - image: nginx:latest&#x000A;    name: pod&#x000A;    ports:&#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;      protocol: TCP&#x000A;```&#x000A;&#x000A;然后就可以执行对应的创建和删除命令了：&#x000A;&#x000A;创建：kubectl create -f pod-nginx.yaml&#x000A;&#x000A;删除：kubectl delete -f pod-nginx.yaml&#x000A;&#x000A;#### 4.3 Label&#x000A;&#x000A;Label是kubernetes系统中的一个重要概念。它的作用就是在资源上添加标识，用来对它们进行区分和选择。&#x000A;&#x000A;Label的特点：&#x000A;&#x000A;- 一个Label会以key/value键值对的形式附加到各种对象上，如Node、Pod、Service等等&#x000A;- 一个资源对象可以定义任意数量的Label ，同一个Label也可以被添加到任意数量的资源对象上去&#x000A;- Label通常在资源对象定义时确定，当然也可以在对象创建后动态添加或者删除&#x000A;&#x000A;可以通过Label实现资源的多维度分组，以便灵活、方便地进行资源分配、调度、配置、部署等管理工作。&#x000A;&#x000A;&gt; 一些常用的Label 示例如下：&#x000A;&gt;&#x000A;&gt; - 版本标签：&quot;version&quot;:&quot;release&quot;, &quot;version&quot;:&quot;stable&quot;......&#x000A;&gt; - 环境标签：&quot;environment&quot;:&quot;dev&quot;，&quot;environment&quot;:&quot;test&quot;，&quot;environment&quot;:&quot;pro&quot;&#x000A;&gt; - 架构标签：&quot;tier&quot;:&quot;frontend&quot;，&quot;tier&quot;:&quot;backend&quot;&#x000A;&#x000A;标签定义完毕之后，还要考虑到标签的选择，这就要使用到Label Selector，即：&#x000A;&#x000A;Label用于给某个资源对象定义标识&#x000A;&#x000A;Label Selector用于查询和筛选拥有某些标签的资源对象&#x000A;&#x000A;当前有两种Label Selector：&#x000A;&#x000A;- 基于等式的Label Selector&#x000A;&#x000A;  name = slave: 选择所有包含Label中key=&quot;name&quot;且value=&quot;slave&quot;的对象&#x000A;&#x000A;  env != production: 选择所有包括Label中的key=&quot;env&quot;且value不等于&quot;production&quot;的对象&#x000A;&#x000A;- 基于集合的Label Selector&#x000A;&#x000A;  name in (master, slave): 选择所有包含Label中的key=&quot;name&quot;且value=&quot;master&quot;或&quot;slave&quot;的对象&#x000A;&#x000A;  name not in (frontend): 选择所有包含Label中的key=&quot;name&quot;且value不等于&quot;frontend&quot;的对象&#x000A;&#x000A;标签的选择条件可以使用多个，此时将多个Label Selector进行组合，使用逗号&quot;,&quot;进行分隔即可。例如：&#x000A;&#x000A;name=slave，env!=production&#x000A;&#x000A;name not in (frontend)，env!=production&#x000A;&#x000A;##### 4.3.1 命令方式&#x000A;&#x000A;```shell&#x000A;# 为pod资源打标签&#x000A;[root@master ~]# kubectl label pod nginx-pod version=1.0 -n dev&#x000A;pod/nginx-pod labeled&#x000A;&#x000A;# 为pod资源更新标签&#x000A;[root@master ~]# kubectl label pod nginx-pod version=2.0 -n dev --overwrite&#x000A;pod/nginx-pod labeled&#x000A;&#x000A;# 查看标签&#x000A;[root@master ~]# kubectl get pod nginx-pod  -n dev --show-labels&#x000A;NAME        READY   STATUS    RESTARTS   AGE   LABELS&#x000A;nginx-pod   1/1     Running   0          10m   version=2.0&#x000A;&#x000A;# 筛选标签&#x000A;[root@master ~]# kubectl get pod -n dev -l version=2.0  --show-labels&#x000A;NAME        READY   STATUS    RESTARTS   AGE   LABELS&#x000A;nginx-pod   1/1     Running   0          17m   version=2.0&#x000A;[root@master ~]# kubectl get pod -n dev -l version!=2.0 --show-labels&#x000A;No resources found in dev namespace.&#x000A;&#x000A;#删除标签&#x000A;[root@master ~]# kubectl label pod nginx-pod -n dev tier-&#x000A;pod/nginx unlabeled&#x000A;```&#x000A;&#x000A;##### 4.3.2 配置方式&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: nginx&#x000A;  namespace: dev&#x000A;  labels:&#x000A;    version: &quot;3.0&quot; &#x000A;    env: &quot;test&quot;&#x000A;spec:&#x000A;  containers:&#x000A;  - image: nginx:latest&#x000A;    name: pod&#x000A;    ports:&#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;      protocol: TCP&#x000A;```&#x000A;&#x000A;然后就可以执行对应的更新命令了：kubectl apply -f pod-nginx.yaml&#x000A;&#x000A;#### 4.4 Deployment&#x000A;&#x000A;在kubernetes中，Pod是最小的控制单元，但是kubernetes很少直接控制Pod，一般都是通过Pod控制器来完成的。Pod控制器用于pod的管理，确保pod资源符合预期的状态，当pod的资源出现故障时，会尝试进行重启或重建pod。&#x000A;&#x000A;在kubernetes中Pod控制器的种类有很多，本章节只介绍一种：Deployment。&#x000A;&#x000A;![image-20200408193950807](Kubenetes.assets/image-20200408193950807.png)&#x000A;&#x000A;##### 4.4.1 命令操作&#x000A;&#x000A;```shell&#x000A;# 命令格式: kubectl create deployment 名称  [参数] &#x000A;# --image  指定pod的镜像&#x000A;# --port   指定端口&#x000A;# --replicas  指定创建pod数量&#x000A;# --namespace  指定namespace&#x000A;[root@master ~]# kubectl run nginx --image=nginx:latest --port=80 --replicas=3 -n dev&#x000A;deployment.apps/nginx created&#x000A;&#x000A;# 查看创建的Pod&#x000A;[root@master ~]# kubectl get pods -n dev&#x000A;NAME                     READY   STATUS    RESTARTS   AGE&#x000A;nginx-5ff7956ff6-6k8cb   1/1     Running   0          19s&#x000A;nginx-5ff7956ff6-jxfjt   1/1     Running   0          19s&#x000A;nginx-5ff7956ff6-v6jqw   1/1     Running   0          19s&#x000A;&#x000A;# 查看deployment的信息&#x000A;[root@master ~]# kubectl get deploy -n dev&#x000A;NAME    READY   UP-TO-DATE   AVAILABLE   AGE&#x000A;nginx   3/3     3            3           2m42s&#x000A;&#x000A;# UP-TO-DATE：成功升级的副本数量&#x000A;# AVAILABLE：可用副本的数量&#x000A;[root@master ~]# kubectl get deploy -n dev -o wide&#x000A;NAME    READY UP-TO-DATE  AVAILABLE   AGE     CONTAINERS   IMAGES              SELECTOR&#x000A;nginx   3/3     3         3           2m51s   nginx        nginx:latest        run=nginx&#x000A;&#x000A;# 查看deployment的详细信息&#x000A;[root@master ~]# kubectl describe deploy nginx -n dev&#x000A;Name:                   nginx&#x000A;Namespace:              dev&#x000A;CreationTimestamp:      Wed, 08 May 2021 11:14:14 +0800&#x000A;Labels:                 run=nginx&#x000A;Annotations:            deployment.kubernetes.io/revision: 1&#x000A;Selector:               run=nginx&#x000A;Replicas:               3 desired | 3 updated | 3 total | 3 available | 0 unavailable&#x000A;StrategyType:           RollingUpdate&#x000A;MinReadySeconds:        0&#x000A;RollingUpdateStrategy:  25% max unavailable, 25% max 违规词汇&#x000A;Pod Template:&#x000A;  Labels:  run=nginx&#x000A;  Containers:&#x000A;   nginx:&#x000A;    Image:        nginx:latest&#x000A;    Port:         80/TCP&#x000A;    Host Port:    0/TCP&#x000A;    Environment:  &lt;none&gt;&#x000A;    Mounts:       &lt;none&gt;&#x000A;  Volumes:        &lt;none&gt;&#x000A;Conditions:&#x000A;  Type           Status  Reason&#x000A;  ----           ------  ------&#x000A;  Available      True    MinimumReplicasAvailable&#x000A;  Progressing    True    NewReplicaSetAvailable&#x000A;OldReplicaSets:  &lt;none&gt;&#x000A;NewReplicaSet:   nginx-5ff7956ff6 (3/3 replicas created)&#x000A;Events:&#x000A;  Type    Reason             Age    From                   Message&#x000A;  ----    ------             ----   ----                   -------&#x000A;  Normal  ScalingReplicaSet  5m43s  deployment-controller  Scaled up replicaset nginx-5ff7956ff6 to 3&#x000A;  &#x000A;# 删除 &#x000A;[root@master ~]# kubectl delete deploy nginx -n dev&#x000A;deployment.apps &quot;nginx&quot; deleted&#x000A;```&#x000A;&#x000A;##### 4.4.2 配置操作&#x000A;&#x000A;创建一个deploy-nginx.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1&#x000A;kind: Deployment&#x000A;metadata:&#x000A;  name: nginx&#x000A;  namespace: dev&#x000A;spec:&#x000A;  replicas: 3&#x000A;  selector:&#x000A;    matchLabels:&#x000A;      run: nginx&#x000A;  template:&#x000A;    metadata:&#x000A;      labels:&#x000A;        run: nginx&#x000A;    spec:&#x000A;      containers:&#x000A;      - image: nginx:latest&#x000A;        name: nginx&#x000A;        ports:&#x000A;        - containerPort: 80&#x000A;          protocol: TCP&#x000A;```&#x000A;&#x000A;然后就可以执行对应的创建和删除命令了：&#x000A;&#x000A;创建：kubectl create -f deploy-nginx.yaml&#x000A;&#x000A;删除：kubectl delete -f deploy-nginx.yaml&#x000A;&#x000A;#### 4.5 Service&#x000A;&#x000A;通过上节课的学习，已经能够利用Deployment来创建一组Pod来提供具有高可用性的服务。&#x000A;&#x000A;虽然每个Pod都会分配一个单独的Pod IP，然而却存在如下两问题：&#x000A;&#x000A;- Pod IP 会随着Pod的重建产生变化&#x000A;- Pod IP 仅仅是集群内可见的虚拟IP，外部无法访问&#x000A;&#x000A;这样对于访问这个服务带来了难度。因此，kubernetes设计了Service来解决这个问题。&#x000A;&#x000A;Service可以看作是一组同类Pod**对外的访问接口**。借助Service，应用可以方便地实现服务发现和负载均衡。&#x000A;&#x000A;![image-20200408194716912](Kubenetes.assets/image-20200408194716912.png)&#x000A;&#x000A;##### 4.5.1 创建集群内部可访问的Service&#x000A;&#x000A;```shell&#x000A;# 暴露Service&#x000A;[root@master ~]# kubectl expose deploy nginx --name=svc-nginx1 --type=ClusterIP --port=80 --target-port=80 -n dev&#x000A;service/svc-nginx1 exposed&#x000A;&#x000A;# 查看service&#x000A;[root@master ~]# kubectl get svc svc-nginx1 -n dev -o wide&#x000A;NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE     SELECTOR&#x000A;svc-nginx1   ClusterIP   10.109.179.231   &lt;none&gt;        80/TCP    3m51s   run=nginx&#x000A;&#x000A;# 这里产生了一个CLUSTER-IP，这就是service的IP，在Service的生命周期中，这个地址是不会变动的&#x000A;# 可以通过这个IP访问当前service对应的POD&#x000A;[root@master ~]# curl 10.109.179.231:80&#x000A;&lt;!DOCTYPE html&gt;&#x000A;&lt;html&gt;&#x000A;&lt;head&gt;&#x000A;&lt;title&gt;Welcome to nginx!&lt;/title&gt;&#x000A;&lt;/head&gt;&#x000A;&lt;body&gt;&#x000A;&lt;h1&gt;Welcome to nginx!&lt;/h1&gt;&#x000A;.......&#x000A;&lt;/body&gt;&#x000A;&lt;/html&gt;&#x000A;```&#x000A;&#x000A;##### 4.5.2 创建集群外部也可访问的Service&#x000A;&#x000A;```shell&#x000A;# 上面创建的Service的type类型为ClusterIP，这个ip地址只用集群内部可访问&#x000A;# 如果需要创建外部也可以访问的Service，需要修改type为NodePort&#x000A;[root@master ~]# kubectl expose deploy nginx --name=svc-nginx2 --type=NodePort --port=80 --target-port=80 -n dev&#x000A;service/svc-nginx2 exposed&#x000A;&#x000A;# 此时查看，会发现出现了NodePort类型的Service，而且有一对Port（80:31928/TC）&#x000A;[root@master ~]# kubectl get svc  svc-nginx2  -n dev -o wide&#x000A;NAME          TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE    SELECTOR&#x000A;svc-nginx2    NodePort    10.100.94.0      &lt;none&gt;        80:31928/TCP   9s     run=nginx&#x000A;&#x000A;# 接下来就可以通过集群外的主机访问 节点IP:31928访问服务了&#x000A;# 例如在的电脑主机上通过浏览器访问下面的地址&#x000A;http://192.168.90.100:31928/&#x000A;```&#x000A;&#x000A;##### 4.5.3 删除Service&#x000A;&#x000A;```shell&#x000A;[root@master ~]# kubectl delete svc svc-nginx-1 -n dev &#x000A;service &quot;svc-nginx-1&quot; deleted&#x000A;```&#x000A;&#x000A;##### 4.5.4 配置方式&#x000A;&#x000A;创建一个svc-nginx.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Service&#x000A;metadata:&#x000A;  name: svc-nginx&#x000A;  namespace: dev&#x000A;spec:&#x000A;  clusterIP: 10.109.179.231 #固定svc的内网ip&#x000A;  ports:&#x000A;  - port: 80&#x000A;    protocol: TCP&#x000A;    targetPort: 80&#x000A;  selector:&#x000A;    run: nginx&#x000A;  type: ClusterIP&#x000A;```&#x000A;&#x000A;然后就可以执行对应的创建和删除命令了：&#x000A;&#x000A;创建：kubectl create -f svc-nginx.yaml&#x000A;&#x000A;删除：kubectl delete -f svc-nginx.yaml&#x000A;&#x000A;&gt; **小结**&#x000A;&gt;&#x000A;&gt; 至此，已经掌握了Namespace、Pod、Deployment、Service资源的基本操作，有了这些操作，就可以在kubernetes集群中实现一个服务的简单部署和访问了，但是如果想要更好的使用kubernetes，就需要深入学习这几种资源的细节和原理。&#x000A;&#x000A;### 5. Pod详解&#x000A;&#x000A;#### 5.1 Pod介绍&#x000A;&#x000A;##### 5.1.1 Pod结构&#x000A;&#x000A;![image-20200407121501907](Kubenetes.assets/image-20200407121501907-1626781151898.png)&#x000A;&#x000A;每个Pod中都可以包含一个或者多个容器，这些容器可以分为两类：&#x000A;&#x000A;- 用户程序所在的容器，数量可多可少&#x000A;&#x000A;- Pause容器，这是每个Pod都会有的一个**根容器**，它的作用有两个：&#x000A;&#x000A;  - 可以以它为依据，评估整个Pod的健康状态&#x000A;&#x000A;  - 可以在根容器上设置Ip地址，其它容器都此Ip（Pod IP），以实现Pod内部的网路通信&#x000A;&#x000A;    ```&#x000A;    这里是Pod内部的通讯，Pod的之间的通讯采用虚拟二层网络技术来实现，我们当前环境用的是Flannel&#x000A;    ```&#x000A;&#x000A;##### 5.1.2 Pod定义&#x000A;&#x000A;下面是Pod的资源清单：&#x000A;&#x000A;```shell&#x000A;apiVersion: v1     #必选，版本号，例如v1&#x000A;kind: Pod       　 #必选，资源类型，例如 Pod&#x000A;metadata:       　 #必选，元数据&#x000A;  name: string     #必选，Pod名称&#x000A;  namespace: string  #Pod所属的命名空间,默认为&quot;default&quot;&#x000A;  labels:       　　  #自定义标签列表&#x000A;    - name: string      　          &#x000A;spec:  #必选，Pod中容器的详细定义&#x000A;  containers:  #必选，Pod中容器列表&#x000A;  - name: string   #必选，容器名称&#x000A;    image: string  #必选，容器的镜像名称&#x000A;    imagePullPolicy: [ Always|Never|IfNotPresent ]  #获取镜像的策略 &#x000A;    command: [string]   #容器的启动命令列表，如不指定，使用打包时使用的启动命令&#x000A;    args: [string]      #容器的启动命令参数列表&#x000A;    workingDir: string  #容器的工作目录&#x000A;    volumeMounts:       #挂载到容器内部的存储卷配置&#x000A;    - name: string      #引用pod定义的共享存储卷的名称，需用volumes[]部分定义的的卷名&#x000A;      mountPath: string #存储卷在容器内mount的绝对路径，应少于512字符&#x000A;      readOnly: boolean #是否为只读模式&#x000A;    ports: #需要暴露的端口库号列表&#x000A;    - name: string        #端口的名称&#x000A;      containerPort: int  #容器需要监听的端口号&#x000A;      hostPort: int       #容器所在主机需要监听的端口号，默认与Container相同&#x000A;      protocol: string    #端口协议，支持TCP和UDP，默认TCP&#x000A;    env:   #容器运行前需设置的环境变量列表&#x000A;    - name: string  #环境变量名称&#x000A;      value: string #环境变量的值&#x000A;    resources: #资源限制和请求的设置&#x000A;      limits:  #资源限制的设置&#x000A;        cpu: string     #Cpu的限制，单位为core数，将用于docker run --cpu-shares参数&#x000A;        memory: string  #内存限制，单位可以为Mib/Gib，将用于docker run --memory参数&#x000A;      requests: #资源请求的设置&#x000A;        cpu: string    #Cpu请求，容器启动的初始可用数量&#x000A;        memory: string #内存请求,容器启动的初始可用数量&#x000A;    lifecycle: #生命周期钩子&#x000A;        postStart: #容器启动后立即执行此钩子,如果执行失败,会根据重启策略进行重启&#x000A;        preStop: #容器终止前执行此钩子,无论结果如何,容器都会终止&#x000A;    livenessProbe:  #对Pod内各容器健康检查的设置，当探测无响应几次后将自动重启该容器&#x000A;      exec:       　 #对Pod容器内检查方式设置为exec方式&#x000A;        command: [string]  #exec方式需要制定的命令或脚本&#x000A;      httpGet:       #对Pod内个容器健康检查方法设置为HttpGet，需要制定Path、port&#x000A;        path: string&#x000A;        port: number&#x000A;        host: string&#x000A;        scheme: string&#x000A;        HttpHeaders:&#x000A;        - name: string&#x000A;          value: string&#x000A;      tcpSocket:     #对Pod内个容器健康检查方式设置为tcpSocket方式&#x000A;         port: number&#x000A;       initialDelaySeconds: 0       #容器启动完成后首次探测的时间，单位为秒&#x000A;       timeoutSeconds: 0    　　    #对容器健康检查探测等待响应的超时时间，单位秒，默认1秒&#x000A;       periodSeconds: 0     　　    #对容器监控检查的定期探测时间设置，单位秒，默认10秒一次&#x000A;       successThreshold: 0&#x000A;       failureThreshold: 0&#x000A;       securityContext:&#x000A;         privileged: false&#x000A;  restartPolicy: [Always | Never | OnFailure]  #Pod的重启策略&#x000A;  nodeName: &lt;string&gt; #设置NodeName表示将该Pod调度到指定到名称的node节点上&#x000A;  nodeSelector: obeject #设置NodeSelector表示将该Pod调度到包含这个label的node上&#x000A;  imagePullSecrets: #Pull镜像时使用的secret名称，以key：secretkey格式指定&#x000A;  - name: string&#x000A;  hostNetwork: false   #是否使用主机网络模式，默认为false，如果设置为true，表示使用宿主机网络&#x000A;  volumes:   #在该pod上定义共享存储卷列表&#x000A;  - name: string    #共享存储卷名称 （volumes类型有很多种）&#x000A;    emptyDir: {}       #类型为emtyDir的存储卷，与Pod同生命周期的一个临时目录。为空值&#x000A;    hostPath: string   #类型为hostPath的存储卷，表示挂载Pod所在宿主机的目录&#x000A;      path: string      　　        #Pod所在宿主机的目录，将被用于同期中mount的目录&#x000A;    secret:       　　　#类型为secret的存储卷，挂载集群与定义的secret对象到容器内部&#x000A;      scretname: string  &#x000A;      items:     &#x000A;      - key: string&#x000A;        path: string&#x000A;    configMap:         #类型为configMap的存储卷，挂载预定义的configMap对象到容器内部&#x000A;      name: string&#x000A;      items:&#x000A;      - key: string&#x000A;        path: string&#x000A;```&#x000A;&#x000A;```shell&#x000A;#小提示：&#x000A;#   在这里，可通过一个命令来查看每种资源的可配置项&#x000A;#   kubectl explain 资源类型         查看某种资源可以配置的一级属性&#x000A;#   kubectl explain 资源类型.属性     查看属性的子属性&#x000A;[root@k8s-master01 ~]# kubectl explain pod&#x000A;KIND:     Pod&#x000A;VERSION:  v1&#x000A;FIELDS:&#x000A;   apiVersion   &lt;string&gt;&#x000A;   kind &lt;string&gt;&#x000A;   metadata     &lt;Object&gt;&#x000A;   spec &lt;Object&gt;&#x000A;   status       &lt;Object&gt;&#x000A;&#x000A;[root@k8s-master01 ~]# kubectl explain pod.metadata&#x000A;KIND:     Pod&#x000A;VERSION:  v1&#x000A;RESOURCE: metadata &lt;Object&gt;&#x000A;FIELDS:&#x000A;   annotations  &lt;map[string]string&gt;&#x000A;   clusterName  &lt;string&gt;&#x000A;   creationTimestamp    &lt;string&gt;&#x000A;   deletionGracePeriodSeconds   &lt;integer&gt;&#x000A;   deletionTimestamp    &lt;string&gt;&#x000A;   finalizers   &lt;[]string&gt;&#x000A;   generateName &lt;string&gt;&#x000A;   generation   &lt;integer&gt;&#x000A;   labels       &lt;map[string]string&gt;&#x000A;   managedFields        &lt;[]Object&gt;&#x000A;   name &lt;string&gt;&#x000A;   namespace    &lt;string&gt;&#x000A;   ownerReferences      &lt;[]Object&gt;&#x000A;   resourceVersion      &lt;string&gt;&#x000A;   selfLink     &lt;string&gt;&#x000A;   uid  &lt;string&gt;&#x000A;```&#x000A;&#x000A;在kubernetes中基本所有资源的一级属性都是一样的，主要包含5部分：&#x000A;&#x000A;- apiVersion &lt;string&gt; 版本，由kubernetes内部定义，版本号必须可以用 kubectl api-versions 查询到&#x000A;- kind &lt;string&gt; 类型，由kubernetes内部定义，版本号必须可以用 kubectl api-resources 查询到&#x000A;- metadata &lt;Object&gt; 元数据，主要是资源标识和说明，常用的有name、namespace、labels等&#x000A;- spec &lt;Object&gt; 描述，这是配置中最重要的一部分，里面是对各种资源配置的详细描述&#x000A;- status &lt;Object&gt; 状态信息，里面的内容不需要定义，由kubernetes自动生成&#x000A;&#x000A;在上面的属性中，spec是接下来研究的重点，继续看下它的常见子属性:&#x000A;&#x000A;- containers &lt;[]Object&gt; 容器列表，用于定义容器的详细信息&#x000A;- nodeName &lt;String&gt; 根据nodeName的值将pod调度到指定的Node节点上&#x000A;- nodeSelector &lt;map[]&gt; 根据NodeSelector中定义的信息选择将该Pod调度到包含这些label的Node 上&#x000A;- hostNetwork &lt;boolean&gt; 是否使用主机网络模式，默认为false，如果设置为true，表示使用宿主机网络&#x000A;- volumes &lt;[]Object&gt; 存储卷，用于定义Pod上面挂在的存储信息&#x000A;- restartPolicy &lt;string&gt; 重启策略，表示Pod在遇到故障的时候的处理策略&#x000A;&#x000A;#### 5.2 Pod配置&#x000A;&#x000A;本小节主要来研究`pod.spec.containers`属性，这也是pod配置中最为关键的一项配置。&#x000A;&#x000A;&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# kubectl explain pod.spec.containers&#x000A;KIND:     Pod&#x000A;VERSION:  v1&#x000A;RESOURCE: containers &lt;[]Object&gt;   # 数组，代表可以有多个容器&#x000A;FIELDS:&#x000A;   name  &lt;string&gt;     # 容器名称&#x000A;   image &lt;string&gt;     # 容器需要的镜像地址&#x000A;   imagePullPolicy  &lt;string&gt; # 镜像拉取策略 &#x000A;   command  &lt;[]string&gt; # 容器的启动命令列表，如不指定，使用打包时使用的启动命令&#x000A;   args     &lt;[]string&gt; # 容器的启动命令需要的参数列表&#x000A;   env      &lt;[]Object&gt; # 容器环境变量的配置&#x000A;   ports    &lt;[]Object&gt;     # 容器需要暴露的端口号列表&#x000A;   resources &lt;Object&gt;      # 资源限制和资源请求的设置&#x000A;```&#x000A;&#x000A;##### 5.2.1 基本配置&#x000A;&#x000A;创建pod-base.yaml文件，内容如下：&#x000A;&#x000A;&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-base&#x000A;  namespace: dev&#x000A;  labels:&#x000A;    user: heima&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  - name: busybox&#x000A;    image: busybox:1.30&#x000A;```&#x000A;&#x000A;![image-20210617223823675](Kubenetes.assets/image-20210617223823675-1626781695411.png)&#x000A;&#x000A;上面定义了一个比较简单Pod的配置，里面有两个容器：&#x000A;&#x000A;- nginx：用1.17.1版本的nginx镜像创建，（nginx是一个轻量级web容器）&#x000A;- busybox：用1.30版本的busybox镜像创建，（busybox是一个小巧的linux命令集合）&#x000A;&#x000A;&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 pod]# kubectl apply -f pod-base.yaml&#x000A;pod/pod-base created&#x000A;&#x000A;# 查看Pod状况&#x000A;# READY 1/2 : 表示当前Pod中有2个容器，其中1个准备就绪，1个未就绪&#x000A;# RESTARTS  : 重启次数，因为有1个容器故障了，Pod一直在重启试图恢复它&#x000A;[root@k8s-master01 pod]# kubectl get pod -n dev&#x000A;NAME       READY   STATUS    RESTARTS   AGE&#x000A;pod-base   1/2     Running   4          95s&#x000A;&#x000A;# 可以通过describe查看内部的详情&#x000A;# 此时已经运行起来了一个基本的Pod，虽然它暂时有问题&#x000A;[root@k8s-master01 pod]# kubectl describe pod pod-base -n dev&#x000A;```&#x000A;&#x000A;##### 5.2.2 镜像拉取&#x000A;&#x000A;创建pod-imagepullpolicy.yaml文件，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-imagepullpolicy&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    imagePullPolicy: Never # 用于设置镜像拉取策略&#x000A;  - name: busybox&#x000A;    image: busybox:1.30&#x000A;```&#x000A;&#x000A;![image-20210617223923659](Kubenetes.assets/image-20210617223923659.png)&#x000A;&#x000A;imagePullPolicy，用于设置镜像拉取策略，kubernetes支持配置三种拉取策略：&#x000A;&#x000A;- Always：总是从远程仓库拉取镜像（一直远程下载）&#x000A;- IfNotPresent：本地有则使用本地镜像，本地没有则从远程仓库拉取镜像（本地有就本地 本地没远程下载）&#x000A;- Never：只使用本地镜像，从不去远程仓库拉取，本地没有就报错 （一直使用本地）&#x000A;&#x000A;&gt; 默认值说明：&#x000A;&gt;&#x000A;&gt; 如果镜像tag为具体版本号， 默认策略是：IfNotPresent&#x000A;&gt;&#x000A;&gt; 如果镜像tag为：latest（最终版本） ，默认策略是always&#x000A;&#x000A;&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 pod]# kubectl create -f pod-imagepullpolicy.yaml&#x000A;pod/pod-imagepullpolicy created&#x000A;&#x000A;# 查看Pod详情&#x000A;# 此时明显可以看到nginx镜像有一步Pulling image &quot;nginx:1.17.1&quot;的过程&#x000A;[root@k8s-master01 pod]# kubectl describe pod pod-imagepullpolicy -n dev&#x000A;......&#x000A;Events:&#x000A;  Type     Reason     Age               From               Message&#x000A;  ----     ------     ----              ----               -------&#x000A;  Normal   Scheduled  &lt;unknown&gt;         default-scheduler  Successfully assigned dev/pod-imagePullPolicy to node1&#x000A;  Normal   Pulling    32s               kubelet, node1     Pulling image &quot;nginx:1.17.1&quot;&#x000A;  Normal   Pulled     26s               kubelet, node1     Successfully pulled image &quot;nginx:1.17.1&quot;&#x000A;  Normal   Created    26s               kubelet, node1     Created container nginx&#x000A;  Normal   Started    25s               kubelet, node1     Started container nginx&#x000A;  Normal   Pulled     7s (x3 over 25s)  kubelet, node1     Container image &quot;busybox:1.30&quot; already present on machine&#x000A;  Normal   Created    7s (x3 over 25s)  kubelet, node1     Created container busybox&#x000A;  Normal   Started    7s (x3 over 25s)  kubelet, node1     Started container busybox&#x000A;```&#x000A;&#x000A;##### 5.2.3 启动命令&#x000A;&#x000A;在前面的案例中，一直有一个问题没有解决，就是的busybox容器一直没有成功运行，那么到底是什么原因导致这个容器的故障呢？&#x000A;&#x000A;原来busybox并不是一个程序，而是类似于一个工具类的集合，kubernetes集群启动管理后，它会自动关闭。解决方法就是让其一直在运行，这就用到了command配置。&#x000A;&#x000A;创建pod-command.yaml文件，内容如下：&#x000A;&#x000A;&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-command&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  - name: busybox&#x000A;    image: busybox:1.30&#x000A;    command: [&quot;/bin/sh&quot;,&quot;-c&quot;,&quot;touch /tmp/hello.txt;while true;do /bin/echo $(date +%T) &gt;&gt; /tmp/hello.txt; sleep 3; done;&quot;]&#x000A;```&#x000A;&#x000A;![image-20210617224457945](Kubenetes.assets/image-20210617224457945.png)&#x000A;&#x000A;command，用于在pod中的容器初始化完毕之后运行一个命令。&#x000A;&#x000A;&gt; 稍微解释下上面命令的意思：&#x000A;&gt;&#x000A;&gt; &quot;/bin/sh&quot;,&quot;-c&quot;, 使用sh执行命令&#x000A;&gt;&#x000A;&gt; touch /tmp/hello.txt; 创建一个/tmp/hello.txt 文件&#x000A;&gt;&#x000A;&gt; while true;do /bin/echo $(date +%T) &gt;&gt; /tmp/hello.txt; sleep 3; done; 每隔3秒向文件中写入当前时间&#x000A;&#x000A;&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 pod]# kubectl create  -f pod-command.yaml&#x000A;pod/pod-command created&#x000A;&#x000A;# 查看Pod状态&#x000A;# 此时发现两个pod都正常运行了&#x000A;[root@k8s-master01 pod]# kubectl get pods pod-command -n dev&#x000A;NAME          READY   STATUS   RESTARTS   AGE&#x000A;pod-command   2/2     Runing   0          2s&#x000A;&#x000A;# 进入pod中的busybox容器，查看文件内容&#x000A;# 补充一个命令: kubectl exec  pod名称 -n 命名空间 -it -c 容器名称 /bin/sh  在容器内部执行命令&#x000A;# 使用这个命令就可以进入某个容器的内部，然后进行相关操作了&#x000A;# 比如，可以查看txt文件的内容&#x000A;[root@k8s-master01 pod]# kubectl exec pod-command -n dev -it -c busybox /bin/sh&#x000A;/ # tail -f /tmp/hello.txt&#x000A;14:44:19&#x000A;14:44:22&#x000A;14:44:25&#x000A;```&#x000A;&#x000A;```&#x000A;特别说明：&#x000A;    通过上面发现command已经可以完成启动命令和传递参数的功能，为什么这里还要提供一个args选项，用于传递参数呢?这其实跟docker有点关系，kubernetes中的command、args两项其实是实现覆盖Dockerfile中ENTRYPOINT的功能。&#x000A; 1 如果command和args均没有写，那么用Dockerfile的配置。&#x000A; 2 如果command写了，但args没有写，那么Dockerfile默认的配置会被忽略，执行输入的command&#x000A; 3 如果command没写，但args写了，那么Dockerfile中配置的ENTRYPOINT的命令会被执行，使用当前args的参数&#x000A; 4 如果command和args都写了，那么Dockerfile的配置被忽略，执行command并追加上args参数&#x000A;```&#x000A;&#x000A;##### 5.2.4 环境变量&#x000A;&#x000A;创建pod-env.yaml文件，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-env&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: busybox&#x000A;    image: busybox:1.30&#x000A;    command: [&quot;/bin/sh&quot;,&quot;-c&quot;,&quot;while true;do /bin/echo $(date +%T);sleep 60; done;&quot;]&#x000A;    env: # 设置环境变量列表&#x000A;    - name: &quot;username&quot;&#x000A;      value: &quot;admin&quot;&#x000A;    - name: &quot;password&quot;&#x000A;      value: &quot;123456&quot;&#x000A;```&#x000A;&#x000A;env，环境变量，用于在pod中的容器设置环境变量。&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-env.yaml&#x000A;pod/pod-env created&#x000A;&#x000A;# 进入容器，输出环境变量&#x000A;[root@k8s-master01 ~]# kubectl exec pod-env -n dev -c busybox -it /bin/sh&#x000A;/ # echo $username&#x000A;admin&#x000A;/ # echo $password&#x000A;123456&#x000A;```&#x000A;&#x000A;这种方式不是很推荐，推荐将这些配置单独存储在配置文件中，这种方式将在后面介绍。&#x000A;&#x000A;##### 5.2.5 端口设置&#x000A;&#x000A;本小节来介绍容器的端口设置，也就是containers的ports选项。&#x000A;&#x000A;首先看下ports支持的子选项：&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# kubectl explain pod.spec.containers.ports&#x000A;KIND:     Pod&#x000A;VERSION:  v1&#x000A;RESOURCE: ports &lt;[]Object&gt;&#x000A;FIELDS:&#x000A;   name         &lt;string&gt;  # 端口名称，如果指定，必须保证name在pod中是唯一的		&#x000A;   containerPort&lt;integer&gt; # 容器要监听的端口(0&lt;x&lt;65536)&#x000A;   hostPort     &lt;integer&gt; # 容器要在主机上公开的端口，如果设置，主机上只能运行容器的一个副本(一般省略) &#x000A;   hostIP       &lt;string&gt;  # 要将外部端口绑定到的主机IP(一般省略)&#x000A;   protocol     &lt;string&gt;  # 端口协议。必须是UDP、TCP或SCTP。默认为“TCP”。&#x000A;```&#x000A;&#x000A;接下来，编写一个测试案例，创建pod-ports.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-ports&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    ports: # 设置容器暴露的端口列表&#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;      protocol: TCP&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-ports.yaml&#x000A;pod/pod-ports created&#x000A;&#x000A;# 查看pod&#x000A;# 在下面可以明显看到配置信息&#x000A;[root@k8s-master01 ~]# kubectl get pod pod-ports -n dev -o yaml&#x000A;......&#x000A;spec:&#x000A;  containers:&#x000A;  - image: nginx:1.17.1&#x000A;    imagePullPolicy: IfNotPresent&#x000A;    name: nginx&#x000A;    ports:&#x000A;    - containerPort: 80&#x000A;      name: nginx-port&#x000A;      protocol: TCP&#x000A;......&#x000A;```&#x000A;&#x000A;访问容器中的程序需要使用的是`Podip:containerPort`&#x000A;&#x000A;##### 5.2.6 资源配额&#x000A;&#x000A;容器中的程序要运行，肯定是要占用一定资源的，比如cpu和内存等，如果不对某个容器的资源做限制，那么它就可能吃掉大量资源，导致其它容器无法运行。针对这种情况，kubernetes提供了对内存和cpu的资源进行配额的机制，这种机制主要通过resources选项实现，他有两个子选项：&#x000A;&#x000A;- limits：用于限制运行时容器的最大占用资源，当容器占用资源超过limits时会被终止，并进行重启&#x000A;- requests ：用于设置容器需要的最小资源，如果环境资源不够，容器将无法启动&#x000A;&#x000A;可以通过上面两个选项设置资源的上下限。&#x000A;&#x000A;接下来，编写一个测试案例，创建pod-resources.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-resources&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    resources: # 资源配额&#x000A;      limits:  # 限制资源（上限）&#x000A;        cpu: &quot;2&quot; # CPU限制，单位是core数&#x000A;        memory: &quot;10Gi&quot; # 内存限制&#x000A;      requests: # 请求资源（下限）&#x000A;        cpu: &quot;1&quot;  # CPU限制，单位是core数&#x000A;        memory: &quot;10Mi&quot;  # 内存限制&#x000A;```&#x000A;&#x000A;在这对cpu和memory的单位做一个说明：&#x000A;&#x000A;- cpu：core数，可以为整数或小数&#x000A;- memory： 内存大小，可以使用Gi、Mi、G、M等形式&#x000A;&#x000A;```shell&#x000A;# 运行Pod&#x000A;[root@k8s-master01 ~]# kubectl create  -f pod-resources.yaml&#x000A;pod/pod-resources created&#x000A;&#x000A;# 查看发现pod运行正常&#x000A;[root@k8s-master01 ~]# kubectl get pod pod-resources -n dev&#x000A;NAME            READY   STATUS    RESTARTS   AGE  &#x000A;pod-resources   1/1     Running   0          39s   &#x000A;&#x000A;# 接下来，停止Pod&#x000A;[root@k8s-master01 ~]# kubectl delete  -f pod-resources.yaml&#x000A;pod &quot;pod-resources&quot; deleted&#x000A;&#x000A;# 编辑pod，修改resources.requests.memory的值为10Gi&#x000A;[root@k8s-master01 ~]# vim pod-resources.yaml&#x000A;&#x000A;# 再次启动pod&#x000A;[root@k8s-master01 ~]# kubectl create  -f pod-resources.yaml&#x000A;pod/pod-resources created&#x000A;&#x000A;# 查看Pod状态，发现Pod启动失败&#x000A;[root@k8s-master01 ~]# kubectl get pod pod-resources -n dev -o wide&#x000A;NAME            READY   STATUS    RESTARTS   AGE          &#x000A;pod-resources   0/1     Pending   0          20s    &#x000A;&#x000A;# 查看pod详情会发现，如下提示&#x000A;[root@k8s-master01 ~]# kubectl describe pod pod-resources -n dev&#x000A;......&#x000A;Warning  FailedScheduling  35s   default-scheduler  0/3 nodes are available: 1 node(s) had taint {node-role.kubernetes.io/master: }, that the pod didn't tolerate, 2 Insufficient memory.(内存不足)&#x000A;```&#x000A;&#x000A;#### 5.3 Pod生命周期&#x000A;&#x000A;我们一般将pod对象从创建至终的这段时间范围称为pod的生命周期，它主要包含下面的过程：&#x000A;&#x000A;- pod创建过程&#x000A;- 运行初始化容器（init container）过程&#x000A;- 运行主容器（main container）&#x000A;  - 容器启动后钩子（post start）、容器终止前钩子（pre stop）&#x000A;  - 容器的存活性探测（liveness probe）、就绪性探测（readiness probe）&#x000A;- pod终止过程&#x000A;&#x000A;![image-20200412111402706](Kubenetes.assets/image-20200412111402706-1626782188724.png)&#x000A;&#x000A;在整个生命周期中，Pod会出现5种**状态**（**相位**），分别如下：&#x000A;&#x000A;- 挂起（Pending）：apiserver已经创建了pod资源对象，但它尚未被调度完成或者仍处于下载镜像的过程中&#x000A;- 运行中（Running）：pod已经被调度至某节点，并且所有容器都已经被kubelet创建完成&#x000A;- 成功（Succeeded）：pod中的所有容器都已经成功终止并且不会被重启&#x000A;- 失败（Failed）：所有容器都已经终止，但至少有一个容器终止失败，即容器返回了非0值的退出状态&#x000A;- 未知（Unknown）：apiserver无法正常获取到pod对象的状态信息，通常由网络通信失败所导致&#x000A;&#x000A;##### 5.3.1 创建和终止&#x000A;&#x000A;**pod的创建过程**&#x000A;&#x000A;1. 用户通过kubectl或其他api客户端提交需要创建的pod信息给apiServer&#x000A;&#x000A;2. apiServer开始生成pod对象的信息，并将信息存入etcd，然后返回确认信息至客户端&#x000A;&#x000A;3. apiServer开始反映etcd中的pod对象的变化，其它组件使用watch机制来跟踪检查apiServer上的变动&#x000A;&#x000A;4. scheduler发现有新的pod对象要创建，开始为Pod分配主机并将结果信息更新至apiServer&#x000A;&#x000A;5. node节点上的kubelet发现有pod调度过来，尝试调用docker启动容器，并将结果回送至apiServer&#x000A;&#x000A;6. apiServer将接收到的pod状态信息存入etcd中&#x000A;&#x000A;   ![image-20200406184656917](Kubenetes.assets/image-20200406184656917-1626782168787.png)&#x000A;&#x000A;**pod的终止过程**&#x000A;&#x000A;1. 用户向apiServer发送删除pod对象的命令&#x000A;2. apiServcer中的pod对象信息会随着时间的推移而更新，在宽限期内（默认30s），pod被视为dead&#x000A;3. 将pod标记为terminating状态&#x000A;4. kubelet在监控到pod对象转为terminating状态的同时启动pod关闭过程&#x000A;5. 端点控制器监控到pod对象的关闭行为时将其从所有匹配到此端点的service资源的端点列表中移除&#x000A;6. 如果当前pod对象定义了preStop钩子处理器，则在其标记为terminating后即会以同步的方式启动执行&#x000A;7. pod对象中的容器进程收到停止信号&#x000A;8. 宽限期结束后，若pod中还存在仍在运行的进程，那么pod对象会收到立即终止的信号&#x000A;9. kubelet请求apiServer将此pod资源的宽限期设置为0从而完成删除操作，此时pod对于用户已不可见&#x000A;&#x000A;##### 5.3.2 初始化容器&#x000A;&#x000A;初始化容器是在pod的主容器启动之前要运行的容器，主要是做一些主容器的前置工作，它具有两大特征：&#x000A;&#x000A;1. 初始化容器必须运行完成直至结束，若某初始化容器运行失败，那么kubernetes需要重启它直到成功完成&#x000A;2. 初始化容器必须按照定义的顺序执行，当且仅当前一个成功之后，后面的一个才能运行&#x000A;&#x000A;初始化容器有很多的应用场景，下面列出的是最常见的几个：&#x000A;&#x000A;- 提供主容器镜像中不具备的工具程序或自定义代码&#x000A;- 初始化容器要先于应用容器串行启动并运行完成，因此可用于延后应用容器的启动直至其依赖的条件得到满足&#x000A;&#x000A;接下来做一个案例，模拟下面这个需求：&#x000A;&#x000A;假设要以主容器来运行nginx，但是要求在运行nginx之前先要能够连接上mysql和redis所在服务器&#x000A;&#x000A;为了简化测试，事先规定好mysql`(192.168.90.14)`和redis`(192.168.90.15)`服务器的地址&#x000A;&#x000A;创建pod-initcontainer.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-initcontainer&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: main-container&#x000A;    image: nginx:1.17.1&#x000A;    ports: &#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;  initContainers:&#x000A;  - name: test-mysql&#x000A;    image: busybox:1.30&#x000A;    command: ['sh', '-c', 'until ping 192.168.90.14 -c 1 ; do echo waiting for mysql...; sleep 2; done;']&#x000A;  - name: test-redis&#x000A;    image: busybox:1.30&#x000A;    command: ['sh', '-c', 'until ping 192.168.90.15 -c 1 ; do echo waiting for reids...; sleep 2; done;']&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-initcontainer.yaml&#x000A;pod/pod-initcontainer created&#x000A;&#x000A;# 查看pod状态&#x000A;# 发现pod卡在启动第一个初始化容器过程中，后面的容器不会运行&#x000A;root@k8s-master01 ~]# kubectl describe pod  pod-initcontainer -n dev&#x000A;........&#x000A;Events:&#x000A;  Type    Reason     Age   From               Message&#x000A;  ----    ------     ----  ----               -------&#x000A;  Normal  Scheduled  49s   default-scheduler  Successfully assigned dev/pod-initcontainer to node1&#x000A;  Normal  Pulled     48s   kubelet, node1     Container image &quot;busybox:1.30&quot; already present on machine&#x000A;  Normal  Created    48s   kubelet, node1     Created container test-mysql&#x000A;  Normal  Started    48s   kubelet, node1     Started container test-mysql&#x000A;&#x000A;# 动态查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-initcontainer -n dev -w&#x000A;NAME                             READY   STATUS     RESTARTS   AGE&#x000A;pod-initcontainer                0/1     Init:0/2   0          15s&#x000A;pod-initcontainer                0/1     Init:1/2   0          52s&#x000A;pod-initcontainer                0/1     Init:1/2   0          53s&#x000A;pod-initcontainer                0/1     PodInitializing   0          89s&#x000A;pod-initcontainer                1/1     Running           0          90s&#x000A;&#x000A;# 接下来新开一个shell，为当前服务器新增两个ip，观察pod的变化&#x000A;[root@k8s-master01 ~]# ifconfig ens33:1 192.168.90.14 netmask 255.255.255.0 up&#x000A;[root@k8s-master01 ~]# ifconfig ens33:2 192.168.90.15 netmask 255.255.255.0 up&#x000A;```&#x000A;&#x000A;##### 5.3.3 钩子函数&#x000A;&#x000A;钩子函数能够感知自身生命周期中的事件，并在相应的时刻到来时运行用户指定的程序代码。&#x000A;&#x000A;kubernetes在主容器的启动之后和停止之前提供了两个钩子函数：&#x000A;&#x000A;- post start：容器创建之后执行，如果失败了会重启容器&#x000A;- pre stop ：容器终止之前执行，执行完成之后容器将成功终止，在其完成之前会阻塞删除容器的操作&#x000A;&#x000A;钩子处理器支持使用下面三种方式定义动作：&#x000A;&#x000A;- Exec命令：在容器内执行一次命令&#x000A;&#x000A;  ```yaml&#x000A;  ……&#x000A;    lifecycle:&#x000A;      postStart: &#x000A;        exec:&#x000A;          command:&#x000A;          - cat&#x000A;          - /tmp/healthy&#x000A;  ……&#x000A;  ```&#x000A;  &#x000A;- TCPSocket：在当前容器尝试访问指定的socket&#x000A;&#x000A;  ```yaml&#x000A;  ……      &#x000A;    lifecycle:&#x000A;      postStart:&#x000A;        tcpSocket:&#x000A;          port: 8080&#x000A;  ……&#x000A;  ```&#x000A;  &#x000A;- HTTPGet：在当前容器中向某url发起http请求&#x000A;&#x000A;  ```yaml&#x000A;  ……&#x000A;    lifecycle:&#x000A;      postStart:&#x000A;        httpGet:&#x000A;          path: / #URI地址&#x000A;          port: 80 #端口号&#x000A;          host: 192.168.5.3 #主机地址&#x000A;          scheme: HTTP #支持的协议，http或者https&#x000A;  ……&#x000A;  ```&#x000A;&#x000A;接下来，以exec方式为例，演示下钩子函数的使用，创建pod-hook-exec.yaml文件，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-hook-exec&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: main-container&#x000A;    image: nginx:1.17.1&#x000A;    ports:&#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;    lifecycle:&#x000A;      postStart: &#x000A;        exec: # 在容器启动的时候执行一个命令，修改掉nginx的默认首页内容&#x000A;          command: [&quot;/bin/sh&quot;, &quot;-c&quot;, &quot;echo postStart... &gt; /usr/share/nginx/html/index.html&quot;]&#x000A;      preStop:&#x000A;        exec: # 在容器停止之前停止nginx服务&#x000A;          command: [&quot;/usr/sbin/nginx&quot;,&quot;-s&quot;,&quot;quit&quot;]&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-hook-exec.yaml&#x000A;pod/pod-hook-exec created&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pods  pod-hook-exec -n dev -o wide&#x000A;NAME           READY   STATUS     RESTARTS   AGE    IP            NODE    &#x000A;pod-hook-exec  1/1     Running    0          29s    10.244.2.48   node2   &#x000A;&#x000A;# 访问pod&#x000A;[root@k8s-master01 ~]# curl 10.244.2.48&#x000A;postStart...&#x000A;```&#x000A;&#x000A;##### 5.3.4 容器探测&#x000A;&#x000A;容器探测用于检测容器中的应用实例是否正常工作，是保障业务可用性的一种传统机制。如果经过探测，实例的状态不符合预期，那么kubernetes就会把该问题实例&quot; 摘除 &quot;，不承担业务流量。kubernetes提供了两种探针来实现容器探测，分别是：&#x000A;&#x000A;- liveness probes：存活性探针，用于检测应用实例当前是否处于正常运行状态，如果不是，k8s会重启容器&#x000A;- readiness probes：就绪性探针，用于检测应用实例当前是否可以接收请求，如果不能，k8s不会转发流量&#x000A;&#x000A;&gt; livenessProbe 决定是否重启容器，readinessProbe 决定是否将请求转发给容器。&#x000A;&#x000A;上面两种探针目前均支持三种探测方式：&#x000A;&#x000A;- Exec命令：在容器内执行一次命令，如果命令执行的退出码为0，则认为程序正常，否则不正常&#x000A;&#x000A;  ```yaml&#x000A;  ……&#x000A;    livenessProbe:&#x000A;      exec:&#x000A;        command:&#x000A;        - cat&#x000A;        - /tmp/healthy&#x000A;  ……&#x000A;  ```&#x000A;  &#x000A;- TCPSocket：将会尝试访问一个用户容器的端口，如果能够建立这条连接，则认为程序正常，否则不正常&#x000A;&#x000A;  ```yaml&#x000A;  ……      &#x000A;    livenessProbe:&#x000A;      tcpSocket:&#x000A;        port: 8080&#x000A;  ……&#x000A;  ```&#x000A;  &#x000A;- HTTPGet：调用容器内Web应用的URL，如果返回的状态码在200和399之间，则认为程序正常，否则不正常&#x000A;&#x000A;  ```yaml&#x000A;  ……&#x000A;    livenessProbe:&#x000A;      httpGet:&#x000A;        path: / #URI地址&#x000A;        port: 80 #端口号&#x000A;        host: 127.0.0.1 #主机地址&#x000A;        scheme: HTTP #支持的协议，http或者https&#x000A;  ……&#x000A;  ```&#x000A;&#x000A;下面以liveness probes为例，做几个演示：&#x000A;&#x000A;**方式一：Exec**&#x000A;&#x000A;创建pod-liveness-exec.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-liveness-exec&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    ports: &#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;    livenessProbe:&#x000A;      exec:&#x000A;        command: [&quot;/bin/cat&quot;,&quot;/tmp/hello.txt&quot;] # 执行一个查看文件的命令&#x000A;```&#x000A;&#x000A;创建pod，观察效果&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-liveness-exec.yaml&#x000A;pod/pod-liveness-exec created&#x000A;&#x000A;# 查看Pod详情&#x000A;[root@k8s-master01 ~]# kubectl describe pods pod-liveness-exec -n dev&#x000A;......&#x000A;  Normal   Created    20s (x2 over 50s)  kubelet, node1     Created container nginx&#x000A;  Normal   Started    20s (x2 over 50s)  kubelet, node1     Started container nginx&#x000A;  Normal   Killing    20s                kubelet, node1     Container nginx failed liveness probe, will be restarted&#x000A;  Warning  Unhealthy  0s (x5 over 40s)   kubelet, node1     Liveness probe failed: cat: can't open '/tmp/hello11.txt': No such file or directory&#x000A;  &#x000A;# 观察上面的信息就会发现nginx容器启动之后就进行了健康检查&#x000A;# 检查失败之后，容器被kill掉，然后尝试进行重启（这是重启策略的作用，后面讲解）&#x000A;# 稍等一会之后，再观察pod信息，就可以看到RESTARTS不再是0，而是一直增长&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-liveness-exec -n dev&#x000A;NAME                READY   STATUS             RESTARTS   AGE&#x000A;pod-liveness-exec   0/1     CrashLoopBackOff   2          3m19s&#x000A;&#x000A;# 当然接下来，可以修改成一个存在的文件，比如/tmp/hello.txt，再试，结果就正常了......&#x000A;```&#x000A;&#x000A;**方式二：TCPSocket**&#x000A;&#x000A;创建pod-liveness-tcpsocket.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-liveness-tcpsocket&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    ports: &#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;    livenessProbe:&#x000A;      tcpSocket:&#x000A;        port: 8080 # 尝试访问8080端口&#x000A;```&#x000A;&#x000A;创建pod，观察效果&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-liveness-tcpsocket.yaml&#x000A;pod/pod-liveness-tcpsocket created&#x000A;&#x000A;# 查看Pod详情&#x000A;[root@k8s-master01 ~]# kubectl describe pods pod-liveness-tcpsocket -n dev&#x000A;......&#x000A;  Normal   Scheduled  31s                            default-scheduler  Successfully assigned dev/pod-liveness-tcpsocket to node2&#x000A;  Normal   Pulled     &lt;invalid&gt;                      kubelet, node2     Container image &quot;nginx:1.17.1&quot; already present on machine&#x000A;  Normal   Created    &lt;invalid&gt;                      kubelet, node2     Created container nginx&#x000A;  Normal   Started    &lt;invalid&gt;                      kubelet, node2     Started container nginx&#x000A;  Warning  Unhealthy  &lt;invalid&gt; (x2 over &lt;invalid&gt;)  kubelet, node2     Liveness probe failed: dial tcp 10.244.2.44:8080: connect: connection refused&#x000A;  &#x000A;# 观察上面的信息，发现尝试访问8080端口,但是失败了&#x000A;# 稍等一会之后，再观察pod信息，就可以看到RESTARTS不再是0，而是一直增长&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-liveness-tcpsocket  -n dev&#x000A;NAME                     READY   STATUS             RESTARTS   AGE&#x000A;pod-liveness-tcpsocket   0/1     CrashLoopBackOff   2          3m19s&#x000A;&#x000A;# 当然接下来，可以修改成一个可以访问的端口，比如80，再试，结果就正常了......&#x000A;```&#x000A;&#x000A;**方式三：HTTPGet**&#x000A;&#x000A;创建pod-liveness-httpget.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-liveness-httpget&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    ports:&#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;    livenessProbe:&#x000A;      httpGet:  # 其实就是访问http://127.0.0.1:80/hello  &#x000A;        scheme: HTTP #支持的协议，http或者https&#x000A;        port: 80 #端口号&#x000A;        path: /hello #URI地址&#x000A;```&#x000A;&#x000A;创建pod，观察效果&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-liveness-httpget.yaml&#x000A;pod/pod-liveness-httpget created&#x000A;&#x000A;# 查看Pod详情&#x000A;[root@k8s-master01 ~]# kubectl describe pod pod-liveness-httpget -n dev&#x000A;.......&#x000A;  Normal   Pulled     6s (x3 over 64s)  kubelet, node1     Container image &quot;nginx:1.17.1&quot; already present on machine&#x000A;  Normal   Created    6s (x3 over 64s)  kubelet, node1     Created container nginx&#x000A;  Normal   Started    6s (x3 over 63s)  kubelet, node1     Started container nginx&#x000A;  Warning  Unhealthy  6s (x6 over 56s)  kubelet, node1     Liveness probe failed: HTTP probe failed with statuscode: 404&#x000A;  Normal   Killing    6s (x2 over 36s)  kubelet, node1     Container nginx failed liveness probe, will be restarted&#x000A;  &#x000A;# 观察上面信息，尝试访问路径，但是未找到,出现404错误&#x000A;# 稍等一会之后，再观察pod信息，就可以看到RESTARTS不再是0，而是一直增长&#x000A;[root@k8s-master01 ~]# kubectl get pod pod-liveness-httpget -n dev&#x000A;NAME                   READY   STATUS    RESTARTS   AGE&#x000A;pod-liveness-httpget   1/1     Running   5          3m17s&#x000A;&#x000A;# 当然接下来，可以修改成一个可以访问的路径path，比如/，再试，结果就正常了......&#x000A;```&#x000A;&#x000A;至此，已经使用liveness Probe演示了三种探测方式，但是查看livenessProbe的子属性，会发现除了这三种方式，还有一些其他的配置，在这里一并解释下：&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# kubectl explain pod.spec.containers.livenessProbe&#x000A;FIELDS:&#x000A;   exec &lt;Object&gt;  &#x000A;   tcpSocket    &lt;Object&gt;&#x000A;   httpGet      &lt;Object&gt;&#x000A;   initialDelaySeconds  &lt;integer&gt;  # 容器启动后等待多少秒执行第一次探测&#x000A;   timeoutSeconds       &lt;integer&gt;  # 探测超时时间。默认1秒，最小1秒&#x000A;   periodSeconds        &lt;integer&gt;  # 执行探测的频率。默认是10秒，最小1秒&#x000A;   failureThreshold     &lt;integer&gt;  # 连续探测失败多少次才被认定为失败。默认是3。最小值是1&#x000A;   successThreshold     &lt;integer&gt;  # 连续探测成功多少次才被认定为成功。默认是1&#x000A;```&#x000A;&#x000A;下面稍微配置两个，演示下效果即可：&#x000A;&#x000A;```yaml&#x000A;[root@k8s-master01 ~]# more pod-liveness-httpget.yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-liveness-httpget&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    ports:&#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;    livenessProbe:&#x000A;      httpGet:&#x000A;        scheme: HTTP&#x000A;        port: 80 &#x000A;        path: /&#x000A;      initialDelaySeconds: 30 # 容器启动后30s开始探测&#x000A;      timeoutSeconds: 5 # 探测超时时间为5s&#x000A;```&#x000A;&#x000A;##### 5.3.5 重启策略&#x000A;&#x000A;在上一节中，一旦容器探测出现了问题，kubernetes就会对容器所在的Pod进行重启，其实这是由pod的重启策略决定的，pod的重启策略有 3 种，分别如下：&#x000A;&#x000A;- Always ：容器失效时，自动重启该容器，这也是默认值。&#x000A;- OnFailure ： 容器终止运行且退出码不为0时重启&#x000A;- Never ： 不论状态为何，都不重启该容器&#x000A;&#x000A;重启策略适用于pod对象中的所有容器，首次需要重启的容器，将在其需要时立即进行重启，随后再次需要重启的操作将由kubelet延迟一段时间后进行，且反复的重启操作的延迟时长以此为10s、20s、40s、80s、160s和300s，300s是最大延迟时长。&#x000A;&#x000A;创建pod-restartpolicy.yaml：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-restartpolicy&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    ports:&#x000A;    - name: nginx-port&#x000A;      containerPort: 80&#x000A;    livenessProbe:&#x000A;      httpGet:&#x000A;        scheme: HTTP&#x000A;        port: 80&#x000A;        path: /hello&#x000A;  restartPolicy: Never # 设置重启策略为Never&#x000A;```&#x000A;&#x000A;运行Pod测试&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-restartpolicy.yaml&#x000A;pod/pod-restartpolicy created&#x000A;&#x000A;# 查看Pod详情，发现nginx容器失败&#x000A;[root@k8s-master01 ~]# kubectl  describe pods pod-restartpolicy  -n dev&#x000A;......&#x000A;  Warning  Unhealthy  15s (x3 over 35s)  kubelet, node1     Liveness probe failed: HTTP probe failed with statuscode: 404&#x000A;  Normal   Killing    15s                kubelet, node1     Container nginx failed liveness probe&#x000A;  &#x000A;# 多等一会，再观察pod的重启次数，发现一直是0，并未重启   &#x000A;[root@k8s-master01 ~]# kubectl  get pods pod-restartpolicy -n dev&#x000A;NAME                   READY   STATUS    RESTARTS   AGE&#x000A;pod-restartpolicy      0/1     Running   0          5min42s&#x000A;```&#x000A;&#x000A;#### 5.4 Pod调度&#x000A;&#x000A;在默认情况下，一个Pod在哪个Node节点上运行，是由Scheduler组件采用相应的算法计算出来的，这个过程是不受人工控制的。但是在实际使用中，这并不满足的需求，因为很多情况下，我们想控制某些Pod到达某些节点上，那么应该怎么做呢？这就要求了解kubernetes对Pod的调度规则，kubernetes提供了四大类调度方式：&#x000A;&#x000A;- 自动调度：运行在哪个节点上完全由Scheduler经过一系列的算法计算得出&#x000A;- 定向调度：NodeName、NodeSelector&#x000A;- 亲和性调度：NodeAffinity、PodAffinity、PodAntiAffinity&#x000A;- 污点（容忍）调度：Taints、Toleration&#x000A;&#x000A;##### 5.4.1 定向调度&#x000A;&#x000A;定向调度，指的是利用在pod上声明nodeName或者nodeSelector，以此将Pod调度到期望的node节点上。注意，这里的调度是强制的，这就意味着即使要调度的目标Node不存在，也会向上面进行调度，只不过pod运行失败而已。&#x000A;&#x000A;**NodeName**&#x000A;&#x000A;NodeName用于强制约束将Pod调度到指定的Name的Node节点上。这种方式，其实是直接跳过Scheduler的调度逻辑，直接将Pod调度到指定名称的节点。&#x000A;&#x000A;接下来，实验一下：创建一个pod-nodename.yaml文件&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-nodename&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  nodeName: node1 # 指定调度到node1节点上&#x000A;```&#x000A;&#x000A;```shell&#x000A;#创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-nodename.yaml&#x000A;pod/pod-nodename created&#x000A;&#x000A;#查看Pod调度到NODE属性，确实是调度到了node1节点上&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-nodename -n dev -o wide&#x000A;NAME           READY   STATUS    RESTARTS   AGE   IP            NODE      ......&#x000A;pod-nodename   1/1     Running   0          56s   10.244.1.87   node1     ......   &#x000A;&#x000A;# 接下来，删除pod，修改nodeName的值为node3（并没有node3节点）&#x000A;[root@k8s-master01 ~]# kubectl delete -f pod-nodename.yaml&#x000A;pod &quot;pod-nodename&quot; deleted&#x000A;[root@k8s-master01 ~]# vim pod-nodename.yaml&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-nodename.yaml&#x000A;pod/pod-nodename created&#x000A;&#x000A;#再次查看，发现已经向Node3节点调度，但是由于不存在node3节点，所以pod无法正常运行&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-nodename -n dev -o wide&#x000A;NAME           READY   STATUS    RESTARTS   AGE   IP       NODE    ......&#x000A;pod-nodename   0/1     Pending   0          6s    &lt;none&gt;   node3   ......           &#x000A;```&#x000A;&#x000A;**NodeSelector**&#x000A;&#x000A;NodeSelector用于将pod调度到添加了指定标签的node节点上。它是通过kubernetes的label-selector机制实现的，也就是说，在pod创建之前，会由scheduler使用MatchNodeSelector调度策略进行label匹配，找出目标node，然后将pod调度到目标节点，该匹配规则是强制约束。&#x000A;&#x000A;接下来，实验一下：&#x000A;&#x000A;1 首先分别为node节点添加标签&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# kubectl label nodes node1 nodeenv=pro&#x000A;node/node2 labeled&#x000A;[root@k8s-master01 ~]# kubectl label nodes node2 nodeenv=test&#x000A;node/node2 labeled&#x000A;```&#x000A;&#x000A;2 创建一个pod-nodeselector.yaml文件，并使用它创建Pod&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-nodeselector&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  nodeSelector: &#x000A;    nodeenv: pro # 指定调度到具有nodeenv=pro标签的节点上&#x000A;```&#x000A;&#x000A;```shell&#x000A;#创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-nodeselector.yaml&#x000A;pod/pod-nodeselector created&#x000A;&#x000A;#查看Pod调度到NODE属性，确实是调度到了node1节点上&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-nodeselector -n dev -o wide&#x000A;NAME               READY   STATUS    RESTARTS   AGE     IP          NODE    ......&#x000A;pod-nodeselector   1/1     Running   0          47s   10.244.1.87   node1   ......&#x000A;&#x000A;# 接下来，删除pod，修改nodeSelector的值为nodeenv: xxxx（不存在打有此标签的节点）&#x000A;[root@k8s-master01 ~]# kubectl delete -f pod-nodeselector.yaml&#x000A;pod &quot;pod-nodeselector&quot; deleted&#x000A;[root@k8s-master01 ~]# vim pod-nodeselector.yaml&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-nodeselector.yaml&#x000A;pod/pod-nodeselector created&#x000A;&#x000A;#再次查看，发现pod无法正常运行,Node的值为none&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -o wide&#x000A;NAME               READY   STATUS    RESTARTS   AGE     IP       NODE    &#x000A;pod-nodeselector   0/1     Pending   0          2m20s   &lt;none&gt;   &lt;none&gt;&#x000A;&#x000A;# 查看详情,发现node selector匹配失败的提示&#x000A;[root@k8s-master01 ~]# kubectl describe pods pod-nodeselector -n dev&#x000A;.......&#x000A;Events:&#x000A;  Type     Reason            Age        From               Message&#x000A;  ----     ------            ----       ----               -------&#x000A;  Warning  FailedScheduling  &lt;unknown&gt;  default-scheduler  0/3 nodes are available: 3 node(s) didn't match node selector.&#x000A;```&#x000A;&#x000A;##### 5.4.2 亲和性调度&#x000A;&#x000A;上一节，介绍了两种定向调度的方式，使用起来非常方便，但是也有一定的问题，那就是如果没有满足条件的Node，那么Pod将不会被运行，即使在集群中还有可用Node列表也不行，这就限制了它的使用场景。&#x000A;&#x000A;基于上面的问题，kubernetes还提供了一种亲和性调度（Affinity）。它在NodeSelector的基础之上的进行了扩展，可以通过配置的形式，实现优先选择满足条件的Node进行调度，如果没有，也可以调度到不满足条件的节点上，使调度更加灵活。&#x000A;&#x000A;Affinity主要分为三类：&#x000A;&#x000A;- nodeAffinity(node亲和性）: 以node为目标，解决pod可以调度到哪些node的问题&#x000A;- podAffinity(pod亲和性) : 以pod为目标，解决pod可以和哪些已存在的pod部署在同一个拓扑域中的问题&#x000A;- podAntiAffinity(pod反亲和性) : 以pod为目标，解决pod不能和哪些已存在pod部署在同一个拓扑域中的问题&#x000A;&#x000A;&gt; 关于亲和性(反亲和性)使用场景的说明：&#x000A;&gt;&#x000A;&gt; **亲和性**：如果两个应用频繁交互，那就有必要利用亲和性让两个应用的尽可能的靠近，这样可以减少因网络通信而带来的性能损耗。&#x000A;&gt;&#x000A;&gt; **反亲和性**：当应用的采用多副本部署时，有必要采用反亲和性让各个应用实例打散分布在各个node上，这样可以提高服务的高可用性。&#x000A;&#x000A;**NodeAffinity**&#x000A;&#x000A;首先来看一下`NodeAffinity`的可配置项：&#x000A;&#x000A;```markdown&#x000A;pod.spec.affinity.nodeAffinity&#x000A;  requiredDuringSchedulingIgnoredDuringExecution  Node节点必须满足指定的所有规则才可以，相当于硬限制&#x000A;    nodeSelectorTerms  节点选择列表&#x000A;      matchFields   按节点字段列出的节点选择器要求列表&#x000A;      matchExpressions   按节点标签列出的节点选择器要求列表(推荐)&#x000A;        key    键&#x000A;        values 值&#x000A;        operat or 关系符 支持Exists, DoesNotExist, In, NotIn, Gt, Lt&#x000A;  preferredDuringSchedulingIgnoredDuringExecution 优先调度到满足指定的规则的Node，相当于软限制 (倾向)&#x000A;    preference   一个节点选择器项，与相应的权重相关联&#x000A;      matchFields   按节点字段列出的节点选择器要求列表&#x000A;      matchExpressions   按节点标签列出的节点选择器要求列表(推荐)&#x000A;        key    键&#x000A;        values 值&#x000A;        operator 关系符 支持In, NotIn, Exists, DoesNotExist, Gt, Lt&#x000A;	weight 倾向权重，在范围1-100。&#x000A;```&#x000A;&#x000A;```shell&#x000A;关系符的使用说明:&#x000A;&#x000A;- matchExpressions:&#x000A;  - key: nodeenv              # 匹配存在标签的key为nodeenv的节点&#x000A;    operator: Exists&#x000A;  - key: nodeenv              # 匹配标签的key为nodeenv,且value是&quot;xxx&quot;或&quot;yyy&quot;的节点&#x000A;    operator: In&#x000A;    values: [&quot;xxx&quot;,&quot;yyy&quot;]&#x000A;  - key: nodeenv              # 匹配标签的key为nodeenv,且value大于&quot;xxx&quot;的节点&#x000A;    operator: Gt&#x000A;    values: &quot;xxx&quot;&#x000A;```&#x000A;&#x000A;接下来首先演示一下`requiredDuringSchedulingIgnoredDuringExecution` ,&#x000A;&#x000A;创建pod-nodeaffinity-required.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-nodeaffinity-required&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  affinity:  #亲和性设置&#x000A;    nodeAffinity: #设置node亲和性&#x000A;      requiredDuringSchedulingIgnoredDuringExecution: # 硬限制&#x000A;        nodeSelectorTerms:&#x000A;        - matchExpressions: # 匹配env的值在[&quot;xxx&quot;,&quot;yyy&quot;]中的标签&#x000A;          - key: nodeenv&#x000A;            operator: In&#x000A;            values: [&quot;xxx&quot;,&quot;yyy&quot;]&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-nodeaffinity-required.yaml&#x000A;pod/pod-nodeaffinity-required created&#x000A;&#x000A;# 查看pod状态 （运行失败）&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-nodeaffinity-required -n dev -o wide&#x000A;NAME                        READY   STATUS    RESTARTS   AGE   IP       NODE    ...... &#x000A;pod-nodeaffinity-required   0/1     Pending   0          16s   &lt;none&gt;   &lt;none&gt;  ......&#x000A;&#x000A;# 查看Pod的详情&#x000A;# 发现调度失败，提示node选择失败&#x000A;[root@k8s-master01 ~]# kubectl describe pod pod-nodeaffinity-required -n dev&#x000A;......&#x000A;  Warning  FailedScheduling  &lt;unknown&gt;  default-scheduler  0/3 nodes are available: 3 node(s) didn't match node selector.&#x000A;  Warning  FailedScheduling  &lt;unknown&gt;  default-scheduler  0/3 nodes are available: 3 node(s) didn't match node selector.&#x000A;&#x000A;#接下来，停止pod&#x000A;[root@k8s-master01 ~]# kubectl delete -f pod-nodeaffinity-required.yaml&#x000A;pod &quot;pod-nodeaffinity-required&quot; deleted&#x000A;&#x000A;# 修改文件，将values: [&quot;xxx&quot;,&quot;yyy&quot;]------&gt; [&quot;pro&quot;,&quot;yyy&quot;]&#x000A;[root@k8s-master01 ~]# vim pod-nodeaffinity-required.yaml&#x000A;&#x000A;# 再次启动&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-nodeaffinity-required.yaml&#x000A;pod/pod-nodeaffinity-required created&#x000A;&#x000A;# 此时查看，发现调度成功，已经将pod调度到了node1上&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-nodeaffinity-required -n dev -o wide&#x000A;NAME                        READY   STATUS    RESTARTS   AGE   IP            NODE  ...... &#x000A;pod-nodeaffinity-required   1/1     Running   0          11s   10.244.1.89   node1 ......&#x000A;```&#x000A;&#x000A;接下来再演示一下`requiredDuringSchedulingIgnoredDuringExecution` ,&#x000A;&#x000A;创建pod-nodeaffinity-preferred.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-nodeaffinity-preferred&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  affinity:  #亲和性设置&#x000A;    nodeAffinity: #设置node亲和性&#x000A;      preferredDuringSchedulingIgnoredDuringExecution: # 软限制&#x000A;      - weight: 1&#x000A;        preference:&#x000A;          matchExpressions: # 匹配env的值在[&quot;xxx&quot;,&quot;yyy&quot;]中的标签(当前环境没有)&#x000A;          - key: nodeenv&#x000A;            operator: In&#x000A;            values: [&quot;xxx&quot;,&quot;yyy&quot;]&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-nodeaffinity-preferred.yaml&#x000A;pod/pod-nodeaffinity-preferred created&#x000A;&#x000A;# 查看pod状态 （运行成功）&#x000A;[root@k8s-master01 ~]# kubectl get pod pod-nodeaffinity-preferred -n dev&#x000A;NAME                         READY   STATUS    RESTARTS   AGE&#x000A;pod-nodeaffinity-preferred   1/1     Running   0          40s&#x000A;```&#x000A;&#x000A;```&#x000A;NodeAffinity规则设置的注意事项：&#x000A;    1 如果同时定义了nodeSelector和nodeAffinity，那么必须两个条件都得到满足，Pod才能运行在指定的Node上&#x000A;    2 如果nodeAffinity指定了多个nodeSelectorTerms，那么只需要其中一个能够匹配成功即可&#x000A;    3 如果一个nodeSelectorTerms中有多个matchExpressions ，则一个节点必须满足所有的才能匹配成功&#x000A;    4 如果一个pod所在的Node在Pod运行期间其标签发生了改变，不再符合该Pod的节点亲和性需求，则系统将忽略此变化&#x000A;```&#x000A;&#x000A;**PodAffinity**&#x000A;&#x000A;PodAffinity主要实现以运行的Pod为参照，实现让新创建的Pod跟参照pod在一个区域的功能。&#x000A;&#x000A;首先来看一下`PodAffinity`的可配置项：&#x000A;&#x000A;```markdown&#x000A;pod.spec.affinity.podAffinity&#x000A;  requiredDuringSchedulingIgnoredDuringExecution  硬限制&#x000A;    namespaces       指定参照pod的namespace&#x000A;    topologyKey      指定调度作用域&#x000A;    labelSelector    标签选择器&#x000A;      matchExpressions  按节点标签列出的节点选择器要求列表(推荐)&#x000A;        key    键&#x000A;        values 值&#x000A;        operator 关系符 支持In, NotIn, Exists, DoesNotExist.&#x000A;      matchLabels    指多个matchExpressions映射的内容&#x000A;  preferredDuringSchedulingIgnoredDuringExecution 软限制&#x000A;    podAffinityTerm  选项&#x000A;      namespaces      &#x000A;      topologyKey&#x000A;      labelSelector&#x000A;        matchExpressions  &#x000A;          key    键&#x000A;          values 值&#x000A;          operator&#x000A;        matchLabels &#x000A;    weight 倾向权重，在范围1-100&#x000A;```&#x000A;&#x000A;```markdown&#x000A;topologyKey用于指定调度时作用域,例如:&#x000A;    如果指定为kubernetes.io/hostname，那就是以Node节点为区分范围&#x000A;	如果指定为beta.kubernetes.io/os,则以Node节点的操作系统类型来区分&#x000A;```&#x000A;&#x000A;接下来，演示下`requiredDuringSchedulingIgnoredDuringExecution`,&#x000A;&#x000A;1）首先创建一个参照Pod，pod-podaffinity-target.yaml：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-podaffinity-target&#x000A;  namespace: dev&#x000A;  labels:&#x000A;    podenv: pro #设置标签&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  nodeName: node1 # 将目标pod名确指定到node1上&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 启动目标pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-podaffinity-target.yaml&#x000A;pod/pod-podaffinity-target created&#x000A;&#x000A;# 查看pod状况&#x000A;[root@k8s-master01 ~]# kubectl get pods  pod-podaffinity-target -n dev&#x000A;NAME                     READY   STATUS    RESTARTS   AGE&#x000A;pod-podaffinity-target   1/1     Running   0          4s&#x000A;```&#x000A;&#x000A;2）创建pod-podaffinity-required.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-podaffinity-required&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  affinity:  #亲和性设置&#x000A;    podAffinity: #设置pod亲和性&#x000A;      requiredDuringSchedulingIgnoredDuringExecution: # 硬限制&#x000A;      - labelSelector:&#x000A;          matchExpressions: # 匹配env的值在[&quot;xxx&quot;,&quot;yyy&quot;]中的标签&#x000A;          - key: podenv&#x000A;            operator: In&#x000A;            values: [&quot;xxx&quot;,&quot;yyy&quot;]&#x000A;        topologyKey: kubernetes.io/hostname&#x000A;```&#x000A;&#x000A;上面配置表达的意思是：新Pod必须要与拥有标签nodeenv=xxx或者nodeenv=yyy的pod在同一Node上，显然现在没有这样pod，接下来，运行测试一下。&#x000A;&#x000A;```shell&#x000A;# 启动pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-podaffinity-required.yaml&#x000A;pod/pod-podaffinity-required created&#x000A;&#x000A;# 查看pod状态，发现未运行&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-podaffinity-required -n dev&#x000A;NAME                       READY   STATUS    RESTARTS   AGE&#x000A;pod-podaffinity-required   0/1     Pending   0          9s&#x000A;&#x000A;# 查看详细信息&#x000A;[root@k8s-master01 ~]# kubectl describe pods pod-podaffinity-required  -n dev&#x000A;......&#x000A;Events:&#x000A;  Type     Reason            Age        From               Message&#x000A;  ----     ------            ----       ----               -------&#x000A;  Warning  FailedScheduling  &lt;unknown&gt;  default-scheduler  0/3 nodes are available: 2 node(s) didn't match pod affinity rules, 1 node(s) had taints that the pod didn't tolerate.&#x000A;&#x000A;# 接下来修改  values: [&quot;xxx&quot;,&quot;yyy&quot;]-----&gt;values:[&quot;pro&quot;,&quot;yyy&quot;]&#x000A;# 意思是：新Pod必须要与拥有标签nodeenv=xxx或者nodeenv=yyy的pod在同一Node上&#x000A;[root@k8s-master01 ~]# vim pod-podaffinity-required.yaml&#x000A;&#x000A;# 然后重新创建pod，查看效果&#x000A;[root@k8s-master01 ~]# kubectl delete -f  pod-podaffinity-required.yaml&#x000A;pod &quot;pod-podaffinity-required&quot; de leted&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-podaffinity-required.yaml&#x000A;pod/pod-podaffinity-required created&#x000A;&#x000A;# 发现此时Pod运行正常&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-podaffinity-required -n dev&#x000A;NAME                       READY   STATUS    RESTARTS   AGE   LABELS&#x000A;pod-podaffinity-required   1/1     Running   0          6s    &lt;none&gt;&#x000A;```&#x000A;&#x000A;关于`PodAffinity`的 `preferredDuringSchedulingIgnoredDuringExecution`，这里不再演示。&#x000A;&#x000A;**PodAntiAffinity**&#x000A;&#x000A;PodAntiAffinity主要实现以运行的Pod为参照，让新创建的Pod跟参照pod不在一个区域中的功能。&#x000A;&#x000A;它的配置方式和选项跟PodAffinty是一样的，这里不再做详细解释，直接做一个测试案例。&#x000A;&#x000A;1）继续使用上个案例中目标pod&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -o wide --show-labels&#x000A;NAME                     READY   STATUS    RESTARTS   AGE     IP            NODE    LABELS&#x000A;pod-podaffinity-required 1/1     Running   0          3m29s   10.244.1.38   node1   &lt;none&gt;     &#x000A;pod-podaffinity-target   1/1     Running   0          9m25s   10.244.1.37   node1   podenv=pro&#x000A;```&#x000A;&#x000A;2）创建pod-podantiaffinity-required.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-podantiaffinity-required&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  affinity:  #亲和性设置&#x000A;    podAntiAffinity: #设置pod亲和性&#x000A;      requiredDuringSchedulingIgnoredDuringExecution: # 硬限制&#x000A;      - labelSelector:&#x000A;          matchExpressions: # 匹配podenv的值在[&quot;pro&quot;]中的标签&#x000A;          - key: podenv&#x000A;            operator: In&#x000A;            values: [&quot;pro&quot;]&#x000A;        topologyKey: kubernetes.io/hostname&#x000A;```&#x000A;&#x000A;上面配置表达的意思是：新Pod必须要与拥有标签nodeenv=pro的pod不在同一Node上，运行测试一下。&#x000A;&#x000A;```shell&#x000A;# 创建pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-podantiaffinity-required.yaml&#x000A;pod/pod-podantiaffinity-required created&#x000A;&#x000A;# 查看pod&#x000A;# 发现调度到了node2上&#x000A;[root@k8s-master01 ~]# kubectl get pods pod-podantiaffinity-required -n dev -o wide&#x000A;NAME                           READY   STATUS    RESTARTS   AGE   IP            NODE   .. &#x000A;pod-podantiaffinity-required   1/1     Running   0          30s   10.244.1.96   node2  ..&#x000A;```&#x000A;&#x000A;##### 5.4.3 污点和容忍&#x000A;&#x000A;**污点（Taints）**&#x000A;&#x000A;前面的调度方式都是站在Pod的角度上，通过在Pod上添加属性，来确定Pod是否要调度到指定的Node上，其实我们也可以站在Node的角度上，通过在Node上添加**污点**属性，来决定是否允许Pod调度过来。&#x000A;&#x000A;Node被设置上污点之后就和Pod之间存在了一种相斥的关系，进而拒绝Pod调度进来，甚至可以将已经存在的Pod驱逐出去。&#x000A;&#x000A;污点的格式为：`key=value:effect`, key和value是污点的标签，effect描述污点的作用，支持如下三个选项：&#x000A;&#x000A;- PreferNoSchedule：kubernetes将尽量避免把Pod调度到具有该污点的Node上，除非没有其他节点可调度&#x000A;- NoSchedule：kubernetes将不会把Pod调度到具有该污点的Node上，但不会影响当前Node上已存在的Pod&#x000A;- NoExecute：kubernetes将不会把Pod调度到具有该污点的Node上，同时也会将Node上已存在的Pod驱离&#x000A;&#x000A;![image-20200605021606508](Kubenetes.assets/image-20200605021831545.png)&#x000A;&#x000A;使用kubectl设置和去除污点的命令示例如下：&#x000A;&#x000A;```shell&#x000A;# 设置污点&#x000A;kubectl taint nodes node1 key=value:effect&#x000A;&#x000A;# 去除污点&#x000A;kubectl taint nodes node1 key:effect-&#x000A;&#x000A;# 去除所有污点&#x000A;kubectl taint nodes node1 key-&#x000A;```&#x000A;&#x000A;接下来，演示下污点的效果：&#x000A;&#x000A;1. 准备节点node1（为了演示效果更加明显，暂时停止node2节点）&#x000A;2. 为node1节点设置一个污点: `tag=heima:PreferNoSchedule`；然后创建pod1( pod1 可以 )&#x000A;3. 修改为node1节点设置一个污点: `tag=heima:NoSchedule`；然后创建pod2( pod1 正常 pod2 失败 )&#x000A;4. 修改为node1节点设置一个污点: `tag=heima:NoExecute`；然后创建pod3 ( 3个pod都失败 )&#x000A;&#x000A;```shell&#x000A;# 为node1设置污点(PreferNoSchedule)&#x000A;[root@k8s-master01 ~]# kubectl taint nodes node1 tag=heima:PreferNoSchedule&#x000A;&#x000A;# 创建pod1&#x000A;[root@k8s-master01 ~]# kubectl run taint1 --image=nginx:1.17.1 -n dev&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -o wide&#x000A;NAME                      READY   STATUS    RESTARTS   AGE     IP           NODE   &#x000A;taint1-7665f7fd85-574h4   1/1     Running   0          2m24s   10.244.1.59   node1    &#x000A;&#x000A;# 为node1设置污点(取消PreferNoSchedule，设置NoSchedule)&#x000A;[root@k8s-master01 ~]# kubectl taint nodes node1 tag:PreferNoSchedule-&#x000A;[root@k8s-master01 ~]# kubectl taint nodes node1 tag=heima:NoSchedule&#x000A;&#x000A;# 创建pod2&#x000A;[root@k8s-master01 ~]# kubectl run taint2 --image=nginx:1.17.1 -n dev&#x000A;[root@k8s-master01 ~]# kubectl get pods taint2 -n dev -o wide&#x000A;NAME                      READY   STATUS    RESTARTS   AGE     IP            NODE&#x000A;taint1-7665f7fd85-574h4   1/1     Running   0          2m24s   10.244.1.59   node1 &#x000A;taint2-544694789-6zmlf    0/1     Pending   0          21s     &lt;none&gt;        &lt;none&gt;   &#x000A;&#x000A;# 为node1设置污点(取消NoSchedule，设置NoExecute)&#x000A;[root@k8s-master01 ~]# kubectl taint nodes node1 tag:NoSchedule-&#x000A;[root@k8s-master01 ~]# kubectl taint nodes node1 tag=heima:NoExecute&#x000A;&#x000A;# 创建pod3&#x000A;[root@k8s-master01 ~]# kubectl run taint3 --image=nginx:1.17.1 -n dev&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -o wide&#x000A;NAME                      READY   STATUS    RESTARTS   AGE   IP       NODE     NOMINATED &#x000A;taint1-7665f7fd85-htkmp   0/1     Pending   0          35s   &lt;none&gt;   &lt;none&gt;   &lt;none&gt;    &#x000A;taint2-544694789-bn7wb    0/1     Pending   0          35s   &lt;none&gt;   &lt;none&gt;   &lt;none&gt;     &#x000A;taint3-6d78dbd749-tktkq   0/1     Pending   0          6s    &lt;none&gt;   &lt;none&gt;   &lt;none&gt;     &#x000A;```&#x000A;&#x000A;```&#x000A;小提示：&#x000A;    使用kubeadm搭建的集群，默认就会给master节点添加一个污点标记,所以pod就不会调度到master节点上.&#x000A;```&#x000A;&#x000A;**容忍（Toleration）**&#x000A;&#x000A;上面介绍了污点的作用，我们可以在node上添加污点用于拒绝pod调度上来，但是如果就是想将一个pod调度到一个有污点的node上去，这时候应该怎么做呢？这就要使用到**容忍**。&#x000A;&#x000A;![image-20200514095913741](Kubenetes.assets/image-20200514095913741.png)&#x000A;&#x000A;&gt; 污点就是拒绝，容忍就是忽略，Node通过污点拒绝pod调度上去，Pod通过容忍忽略拒绝&#x000A;&#x000A;下面先通过一个案例看下效果：&#x000A;&#x000A;1. 上一小节，已经在node1节点上打上了`NoExecute`的污点，此时pod是调度不上去的&#x000A;2. 本小节，可以通过给pod添加容忍，然后将其调度上去&#x000A;&#x000A;创建pod-toleration.yaml,内容如下&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-toleration&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;  tolerations:      # 添加容忍&#x000A;  - key: &quot;tag&quot;        # 要容忍的污点的key&#x000A;    operator: &quot;Equal&quot; # 操作符&#x000A;    value: &quot;heima&quot;    # 容忍的污点的value&#x000A;    effect: &quot;NoExecute&quot;   # 添加容忍的规则，这里必须和标记的污点规则相同&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 添加容忍之前的pod&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -o wide&#x000A;NAME             READY   STATUS    RESTARTS   AGE   IP       NODE     NOMINATED &#x000A;pod-toleration   0/1     Pending   0          3s    &lt;none&gt;   &lt;none&gt;   &lt;none&gt;           &#x000A;&#x000A;# 添加容忍之后的pod&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -o wide&#x000A;NAME             READY   STATUS    RESTARTS   AGE   IP            NODE    NOMINATED&#x000A;pod-toleration   1/1     Running   0          3s    10.244.1.62   node1   &lt;none&gt;        &#x000A;```&#x000A;&#x000A;下面看一下容忍的详细配置:&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# kubectl explain pod.spec.tolerations&#x000A;......&#x000A;FIELDS:&#x000A;   key       # 对应着要容忍的污点的键，空意味着匹配所有的键&#x000A;   value     # 对应着要容忍的污点的值&#x000A;   operator  # key-value的运算符，支持Equal和Exists（默认）&#x000A;   effect    # 对应污点的effect，空意味着匹配所有影响&#x000A;   tolerationSeconds   # 容忍时间, 当effect为NoExecute时生效，表示pod在Node上的停留时间&#x000A;```&#x000A;&#x000A; &#x000A;&#x000A;### 6. Pod控制器详解&#x000A;&#x000A;#### 6.1 Pod控制器介绍&#x000A;&#x000A;Pod是kubernetes的最小管理单元，在kubernetes中，按照pod的创建方式可以将其分为两类：&#x000A;&#x000A;- 自主式pod：kubernetes直接创建出来的Pod，这种pod删除后就没有了，也不会重建&#x000A;- 控制器创建的pod：kubernetes通过控制器创建的pod，这种pod删除了之后还会自动重建&#x000A;&#x000A;&gt; **`什么是Pod控制器`**&#x000A;&gt;&#x000A;&gt; Pod控制器是管理pod的中间层，使用Pod控制器之后，只需要告诉Pod控制器，想要多少个什么样的Pod就可以了，它会创建出满足条件的Pod并确保每一个Pod资源处于用户期望的目标状态。如果Pod资源在运行中出现故障，它会基于指定策略重新编排Pod。&#x000A;&#x000A;在kubernetes中，有很多类型的pod控制器，每种都有自己的适合的场景，常见的有下面这些：&#x000A;&#x000A;- ReplicationController：比较原始的pod控制器，已经被废弃，由ReplicaSet替代&#x000A;- ReplicaSet：保证副本数量一直维持在期望值，并支持pod数量扩缩容，镜像版本升级&#x000A;- Deployment：通过控制ReplicaSet来控制Pod，并支持滚动升级、回退版本&#x000A;- Horizontal Pod Autoscaler：可以根据集群负载自动水平调整Pod的数量，实现削峰填谷&#x000A;- DaemonSet：在集群中的指定Node上运行且仅运行一个副本，一般用于守护进程类的任务&#x000A;- Job：它创建出来的pod只要完成任务就立即退出，不需要重启或重建，用于执行一次性任务&#x000A;- Cronjob：它创建的Pod负责周期性任务控制，不需要持续后台运行&#x000A;- StatefulSet：管理有状态应用&#x000A;&#x000A;#### 6.2 ReplicaSet(RS)&#x000A;&#x000A;ReplicaSet的主要作用是**保证一定数量的pod正常运行**，它会持续监听这些Pod的运行状态，一旦Pod发生故障，就会重启或重建。同时它还支持对pod数量的扩缩容和镜像版本的升降级。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200612005334159.png)&#x000A;&#x000A;ReplicaSet的资源清单文件：&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1 # 版本号&#x000A;kind: ReplicaSet # 类型       &#x000A;metadata: # 元数据&#x000A;  name: # rs名称 &#x000A;  namespace: # 所属命名空间 &#x000A;  labels: #标签&#x000A;    controller: rs&#x000A;spec: # 详情描述&#x000A;  replicas: 3 # 副本数量&#x000A;  selector: # 选择器，通过它指定该控制器管理哪些pod&#x000A;    matchLabels:      # Labels匹配规则&#x000A;      app: nginx-pod&#x000A;    matchExpressions: # Expressions匹配规则&#x000A;      - {key: app, operator: In, values: [nginx-pod]}&#x000A;  template: # 模板，当副本数量不足时，会根据下面的模板创建pod副本&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: nginx-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: nginx&#x000A;        image: nginx:1.17.1&#x000A;        ports:&#x000A;        - containerPort: 80&#x000A;```&#x000A;&#x000A;在这里面，需要新了解的配置项就是`spec`下面几个选项：&#x000A;&#x000A;- replicas：指定副本数量，其实就是当前rs创建出来的pod的数量，默认为1&#x000A;&#x000A;- selector：选择器，它的作用是建立pod控制器和pod之间的关联关系，采用的Label Selector机制&#x000A;&#x000A;  在pod模板上定义label，在控制器上定义选择器，就可以表明当前控制器能管理哪些pod了&#x000A;&#x000A;- template：模板，就是当前控制器创建pod所使用的模板板，里面其实就是前一章学过的pod的定义&#x000A;&#x000A;**创建ReplicaSet**&#x000A;&#x000A;创建pc-replicaset.yaml文件，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1&#x000A;kind: ReplicaSet   &#x000A;metadata:&#x000A;  name: pc-replicaset&#x000A;  namespace: dev&#x000A;spec:&#x000A;  replicas: 3&#x000A;  selector: &#x000A;    matchLabels:&#x000A;      app: nginx-pod&#x000A;  template:&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: nginx-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: nginx&#x000A;        image: nginx:1.17.1&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建rs&#x000A;[root@k8s-master01 ~]# kubectl create -f pc-replicaset.yaml&#x000A;replicaset.apps/pc-replicaset created&#x000A;&#x000A;# 查看rs&#x000A;# DESIRED:期望副本数量  &#x000A;# CURRENT:当前副本数量  &#x000A;# READY:已经准备好提供服务的副本数量&#x000A;[root@k8s-master01 ~]# kubectl get rs pc-replicaset -n dev -o wide&#x000A;NAME          DESIRED   CURRENT READY AGE   CONTAINERS   IMAGES             SELECTOR&#x000A;pc-replicaset 3         3       3     22s   nginx        nginx:1.17.1       app=nginx-pod&#x000A;&#x000A;# 查看当前控制器创建出来的pod&#x000A;# 这里发现控制器创建出来的pod的名称是在控制器名称后面拼接了-xxxxx随机码&#x000A;[root@k8s-master01 ~]# kubectl get pod -n dev&#x000A;NAME                          READY   STATUS    RESTARTS   AGE&#x000A;pc-replicaset-6vmvt   1/1     Running   0          54s&#x000A;pc-replicaset-fmb8f   1/1     Running   0          54s&#x000A;pc-replicaset-snrk2   1/1     Running   0          54s&#x000A;```&#x000A;&#x000A;**扩缩容**&#x000A;&#x000A;```shell&#x000A;# 编辑rs的副本数量，修改spec:replicas: 6即可&#x000A;[root@k8s-master01 ~]# kubectl edit rs pc-replicaset -n dev&#x000A;replicaset.apps/pc-replicaset edited&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev&#x000A;NAME                          READY   STATUS    RESTARTS   AGE&#x000A;pc-replicaset-6vmvt   1/1     Running   0          114m&#x000A;pc-replicaset-cftnp   1/1     Running   0          10s&#x000A;pc-replicaset-fjlm6   1/1     Running   0          10s&#x000A;pc-replicaset-fmb8f   1/1     Running   0          114m&#x000A;pc-replicaset-s2whj   1/1     Running   0          10s&#x000A;pc-replicaset-snrk2   1/1     Running   0          114m&#x000A;&#x000A;# 当然也可以直接使用命令实现&#x000A;# 使用scale命令实现扩缩容， 后面--replicas=n直接指定目标数量即可&#x000A;[root@k8s-master01 ~]# kubectl scale rs pc-replicaset --replicas=2 -n dev&#x000A;replicaset.apps/pc-replicaset scaled&#x000A;&#x000A;# 命令运行完毕，立即查看，发现已经有4个开始准备退出了&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev&#x000A;NAME                       READY   STATUS        RESTARTS   AGE&#x000A;pc-replicaset-6vmvt   0/1     Terminating   0          118m&#x000A;pc-replicaset-cftnp   0/1     Terminating   0          4m17s&#x000A;pc-replicaset-fjlm6   0/1     Terminating   0          4m17s&#x000A;pc-replicaset-fmb8f   1/1     Running       0          118m&#x000A;pc-replicaset-s2whj   0/1     Terminating   0          4m17s&#x000A;pc-replicaset-snrk2   1/1     Running       0          118m&#x000A;&#x000A;#稍等片刻，就只剩下2个了&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev&#x000A;NAME                       READY   STATUS    RESTARTS   AGE&#x000A;pc-replicaset-fmb8f   1/1     Running   0          119m&#x000A;pc-replicaset-snrk2   1/1     Running   0          119m&#x000A;```&#x000A;&#x000A;**镜像升级**&#x000A;&#x000A;```shell&#x000A;# 编辑rs的容器镜像 - image: nginx:1.17.2&#x000A;[root@k8s-master01 ~]# kubectl edit rs pc-replicaset -n dev&#x000A;replicaset.apps/pc-replicaset edited&#x000A;&#x000A;# 再次查看，发现镜像版本已经变更了&#x000A;[root@k8s-master01 ~]# kubectl get rs -n dev -o wide&#x000A;NAME                DESIRED  CURRENT   READY   AGE    CONTAINERS   IMAGES        ...&#x000A;pc-replicaset       2        2         2       140m   nginx         nginx:1.17.2  ...&#x000A;&#x000A;# 同样的道理，也可以使用命令完成这个工作&#x000A;# kubectl set image rs rs名称 容器=镜像版本 -n namespace&#x000A;[root@k8s-master01 ~]# kubectl set image rs pc-replicaset nginx=nginx:1.17.1  -n dev&#x000A;replicaset.apps/pc-replicaset image updated&#x000A;&#x000A;# 再次查看，发现镜像版本已经变更了&#x000A;[root@k8s-master01 ~]# kubectl get rs -n dev -o wide&#x000A;NAME                 DESIRED  CURRENT   READY   AGE    CONTAINERS   IMAGES            ...&#x000A;pc-replicaset        2        2         2       145m   nginx        nginx:1.17.1 ... &#x000A;```&#x000A;&#x000A;**删除ReplicaSet**&#x000A;&#x000A;```shell&#x000A;# 使用kubectl delete命令会删除此RS以及它管理的Pod&#x000A;# 在kubernetes删除RS前，会将RS的replicasclear调整为0，等待所有的Pod被删除后，在执行RS对象的删除&#x000A;[root@k8s-master01 ~]# kubectl delete rs pc-replicaset -n dev&#x000A;replicaset.apps &quot;pc-replicaset&quot; deleted&#x000A;[root@k8s-master01 ~]# kubectl get pod -n dev -o wide&#x000A;No resources found in dev namespace.&#x000A;&#x000A;# 如果希望仅仅删除RS对象（保留Pod），可以使用kubectl delete命令时添加--cascade=false选项（不推荐）。&#x000A;[root@k8s-master01 ~]# kubectl delete rs pc-replicaset -n dev --cascade=false&#x000A;replicaset.apps &quot;pc-replicaset&quot; deleted&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev&#x000A;NAME                  READY   STATUS    RESTARTS   AGE&#x000A;pc-replicaset-cl82j   1/1     Running   0          75s&#x000A;pc-replicaset-dslhb   1/1     Running   0          75s&#x000A;&#x000A;# 也可以使用yaml直接删除(推荐)&#x000A;[root@k8s-master01 ~]# kubectl delete -f pc-replicaset.yaml&#x000A;replicaset.apps &quot;pc-replicaset&quot; deleted&#x000A;```&#x000A;&#x000A;#### 6.3 Deployment(Deploy)&#x000A;&#x000A;为了更好的解决服务编排的问题，kubernetes在V1.2版本开始，引入了Deployment控制器。值得一提的是，这种控制器并不直接管理pod，而是通过管理ReplicaSet来简介管理Pod，即：Deployment管理ReplicaSet，ReplicaSet管理Pod。所以Deployment比ReplicaSet功能更加强大。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200612005524778.png)&#x000A;&#x000A;Deployment主要功能有下面几个：&#x000A;&#x000A;- 支持ReplicaSet的所有功能&#x000A;- 支持发布的停止、继续&#x000A;- 支持滚动升级和回滚版本&#x000A;&#x000A;Deployment的资源清单文件：&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1 # 版本号&#x000A;kind: Deployment # 类型       &#x000A;metadata: # 元数据&#x000A;  name: # rs名称 &#x000A;  namespace: # 所属命名空间 &#x000A;  labels: #标签&#x000A;    controller: deploy&#x000A;spec: # 详情描述&#x000A;  replicas: 3 # 副本数量&#x000A;  revisionHistoryLimit: 3 # 保留历史版本&#x000A;  paused: false # 暂停部署，默认是false&#x000A;  progressDeadlineSeconds: 600 # 部署超时时间（s），默认是600&#x000A;  strategy: # 策略&#x000A;    type: RollingUpdate # 滚动更新策略&#x000A;    rollingUpdate: # 滚动更新&#x000A;      max违规词汇: 30% # 最大额外可以存在的副本数，可以为百分比，也可以为整数&#x000A;      maxUnavailable: 30% # 最大不可用状态的 Pod 的最大值，可以为百分比，也可以为整数&#x000A;  selector: # 选择器，通过它指定该控制器管理哪些pod&#x000A;    matchLabels:      # Labels匹配规则&#x000A;      app: nginx-pod&#x000A;    matchExpressions: # Expressions匹配规则&#x000A;      - {key: app, operator: In, values: [nginx-pod]}&#x000A;  template: # 模板，当副本数量不足时，会根据下面的模板创建pod副本&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: nginx-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: nginx&#x000A;        image: nginx:1.17.1&#x000A;        ports:&#x000A;        - containerPort: 80&#x000A;```&#x000A;&#x000A;##### 6.3.1 创建deployment&#x000A;&#x000A;创建pc-deployment.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1&#x000A;kind: Deployment      &#x000A;metadata:&#x000A;  name: pc-deployment&#x000A;  namespace: dev&#x000A;spec: &#x000A;  replicas: 3&#x000A;  selector:&#x000A;    matchLabels:&#x000A;      app: nginx-pod&#x000A;  template:&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: nginx-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: nginx&#x000A;        image: nginx:1.17.1&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建deployment&#x000A;[root@k8s-master01 ~]# kubectl create -f pc-deployment.yaml --record=true&#x000A;deployment.apps/pc-deployment created&#x000A;&#x000A;# 查看deployment&#x000A;# UP-TO-DATE 最新版本的pod的数量&#x000A;# AVAILABLE  当前可用的pod的数量&#x000A;[root@k8s-master01 ~]# kubectl get deploy pc-deployment -n dev&#x000A;NAME            READY   UP-TO-DATE   AVAILABLE   AGE&#x000A;pc-deployment   3/3     3            3           15s&#x000A;&#x000A;# 查看rs&#x000A;# 发现rs的名称是在原来deployment的名字后面添加了一个10位数的随机串&#x000A;[root@k8s-master01 ~]# kubectl get rs -n dev&#x000A;NAME                       DESIRED   CURRENT   READY   AGE&#x000A;pc-deployment-6696798b78   3         3         3       23s&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev&#x000A;NAME                             READY   STATUS    RESTARTS   AGE&#x000A;pc-deployment-6696798b78-d2c8n   1/1     Running   0          107s&#x000A;pc-deployment-6696798b78-smpvp   1/1     Running   0          107s&#x000A;pc-deployment-6696798b78-wvjd8   1/1     Running   0          107s&#x000A;```&#x000A;&#x000A;##### 6.3.2 扩缩容&#x000A;&#x000A;```shell&#x000A;# 变更副本数量为5个&#x000A;[root@k8s-master01 ~]# kubectl scale deploy pc-deployment --replicas=5  -n dev&#x000A;deployment.apps/pc-deployment scaled&#x000A;&#x000A;# 查看deployment&#x000A;[root@k8s-master01 ~]# kubectl get deploy pc-deployment -n dev&#x000A;NAME            READY   UP-TO-DATE   AVAILABLE   AGE&#x000A;pc-deployment   5/5     5            5           2m&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]#  kubectl get pods -n dev&#x000A;NAME                             READY   STATUS    RESTARTS   AGE&#x000A;pc-deployment-6696798b78-d2c8n   1/1     Running   0          4m19s&#x000A;pc-deployment-6696798b78-jxmdq   1/1     Running   0          94s&#x000A;pc-deployment-6696798b78-mktqv   1/1     Running   0          93s&#x000A;pc-deployment-6696798b78-smpvp   1/1     Running   0          4m19s&#x000A;pc-deployment-6696798b78-wvjd8   1/1     Running   0          4m19s&#x000A;&#x000A;# 编辑deployment的副本数量，修改spec:replicas: 4即可&#x000A;[root@k8s-master01 ~]# kubectl edit deploy pc-deployment -n dev&#x000A;deployment.apps/pc-deployment edited&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev&#x000A;NAME                             READY   STATUS    RESTARTS   AGE&#x000A;pc-deployment-6696798b78-d2c8n   1/1     Running   0          5m23s&#x000A;pc-deployment-6696798b78-jxmdq   1/1     Running   0          2m38s&#x000A;pc-deployment-6696798b78-smpvp   1/1     Running   0          5m23s&#x000A;pc-deployment-6696798b78-wvjd8   1/1     Running   0          5m23s&#x000A;```&#x000A;&#x000A;**镜像更新**&#x000A;&#x000A;deployment支持两种更新策略:`重建更新`和`滚动更新`,可以通过`strategy`指定策略类型,支持两个属性:&#x000A;&#x000A;```markdown&#x000A;strategy：指定新的Pod替换旧的Pod的策略， 支持两个属性：&#x000A;  type：指定策略类型，支持两种策略&#x000A;    Recreate：在创建出新的Pod之前会先杀掉所有已存在的Pod&#x000A;    RollingUpdate：滚动更新，就是杀死一部分，就启动一部分，在更新过程中，存在两个版本Pod&#x000A;  rollingUpdate：当type为RollingUpdate时生效，用于为RollingUpdate设置参数，支持两个属性：&#x000A;    maxUnavailable：用来指定在升级过程中不可用Pod的最大数量，默认为25%。&#x000A;    max违规词汇： 用来指定在升级过程中可以超过期望的Pod的最大数量，默认为25%。&#x000A;```&#x000A;&#x000A;重建更新&#x000A;&#x000A;1) 编辑pc-deployment.yaml,在spec节点下添加更新策略&#x000A;&#x000A;```yaml&#x000A;spec:&#x000A;  strategy: # 策略&#x000A;    type: Recreate # 重建更新&#x000A;```&#x000A;&#x000A;2) 创建deploy进行验证&#x000A;&#x000A;```shell&#x000A;# 变更镜像&#x000A;[root@k8s-master01 ~]# kubectl set image deployment pc-deployment nginx=nginx:1.17.2 -n dev&#x000A;deployment.apps/pc-deployment image updated&#x000A;&#x000A;# 观察升级过程&#x000A;[root@k8s-master01 ~]#  kubectl get pods -n dev -w&#x000A;NAME                             READY   STATUS    RESTARTS   AGE&#x000A;pc-deployment-5d89bdfbf9-65qcw   1/1     Running   0          31s&#x000A;pc-deployment-5d89bdfbf9-w5nzv   1/1     Running   0          31s&#x000A;pc-deployment-5d89bdfbf9-xpt7w   1/1     Running   0          31s&#x000A;&#x000A;pc-deployment-5d89bdfbf9-xpt7w   1/1     Terminating   0          41s&#x000A;pc-deployment-5d89bdfbf9-65qcw   1/1     Terminating   0          41s&#x000A;pc-deployment-5d89bdfbf9-w5nzv   1/1     Terminating   0          41s&#x000A;&#x000A;pc-deployment-675d469f8b-grn8z   0/1     Pending       0          0s&#x000A;pc-deployment-675d469f8b-hbl4v   0/1     Pending       0          0s&#x000A;pc-deployment-675d469f8b-67nz2   0/1     Pending       0          0s&#x000A;&#x000A;pc-deployment-675d469f8b-grn8z   0/1     ContainerCreating   0          0s&#x000A;pc-deployment-675d469f8b-hbl4v   0/1     ContainerCreating   0          0s&#x000A;pc-deployment-675d469f8b-67nz2   0/1     ContainerCreating   0          0s&#x000A;&#x000A;pc-deployment-675d469f8b-grn8z   1/1     Running             0          1s&#x000A;pc-deployment-675d469f8b-67nz2   1/1     Running             0          1s&#x000A;pc-deployment-675d469f8b-hbl4v   1/1     Running             0          2s&#x000A;```&#x000A;&#x000A;滚动更新&#x000A;&#x000A;1) 编辑pc-deployment.yaml,在spec节点下添加更新策略&#x000A;&#x000A;```yaml&#x000A;spec:&#x000A;  strategy: # 策略&#x000A;    type: RollingUpdate # 滚动更新策略&#x000A;    rollingUpdate:&#x000A;      max违规词汇: 25% &#x000A;      maxUnavailable: 25%&#x000A;```&#x000A;&#x000A;2) 创建deploy进行验证&#x000A;&#x000A;```shell&#x000A;# 变更镜像&#x000A;[root@k8s-master01 ~]# kubectl set image deployment pc-deployment nginx=nginx:1.17.3 -n dev &#x000A;deployment.apps/pc-deployment image updated&#x000A;&#x000A;# 观察升级过程&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -w&#x000A;NAME                           READY   STATUS    RESTARTS   AGE&#x000A;pc-deployment-c848d767-8rbzt   1/1     Running   0          31m&#x000A;pc-deployment-c848d767-h4p68   1/1     Running   0          31m&#x000A;pc-deployment-c848d767-hlmz4   1/1     Running   0          31m&#x000A;pc-deployment-c848d767-rrqcn   1/1     Running   0          31m&#x000A;&#x000A;pc-deployment-966bf7f44-226rx   0/1     Pending             0          0s&#x000A;pc-deployment-966bf7f44-226rx   0/1     ContainerCreating   0          0s&#x000A;pc-deployment-966bf7f44-226rx   1/1     Running             0          1s&#x000A;pc-deployment-c848d767-h4p68    0/1     Terminating         0          34m&#x000A;&#x000A;pc-deployment-966bf7f44-cnd44   0/1     Pending             0          0s&#x000A;pc-deployment-966bf7f44-cnd44   0/1     ContainerCreating   0          0s&#x000A;pc-deployment-966bf7f44-cnd44   1/1     Running             0          2s&#x000A;pc-deployment-c848d767-hlmz4    0/1     Terminating         0          34m&#x000A;&#x000A;pc-deployment-966bf7f44-px48p   0/1     Pending             0          0s&#x000A;pc-deployment-966bf7f44-px48p   0/1     ContainerCreating   0          0s&#x000A;pc-deployment-966bf7f44-px48p   1/1     Running             0          0s&#x000A;pc-deployment-c848d767-8rbzt    0/1     Terminating         0          34m&#x000A;&#x000A;pc-deployment-966bf7f44-dkmqp   0/1     Pending             0          0s&#x000A;pc-deployment-966bf7f44-dkmqp   0/1     ContainerCreating   0          0s&#x000A;pc-deployment-966bf7f44-dkmqp   1/1     Running             0          2s&#x000A;pc-deployment-c848d767-rrqcn    0/1     Terminating         0          34m&#x000A;&#x000A;# 至此，新版本的pod创建完毕，就版本的pod销毁完毕&#x000A;# 中间过程是滚动进行的，也就是边销毁边创建&#x000A;```&#x000A;&#x000A;滚动更新的过程：&#x000A;&#x000A;![img](Kubenetes.assets/image-20200416140251491.png)&#x000A;&#x000A;镜像更新中rs的变化&#x000A;&#x000A;```shell&#x000A;# 查看rs,发现原来的rs的依旧存在，只是pod数量变为了0，而后又新产生了一个rs，pod数量为4&#x000A;# 其实这就是deployment能够进行版本回退的奥妙所在，后面会详细解释&#x000A;[root@k8s-master01 ~]# kubectl get rs -n dev&#x000A;NAME                       DESIRED   CURRENT   READY   AGE&#x000A;pc-deployment-6696798b78   0         0         0       7m37s&#x000A;pc-deployment-6696798b11   0         0         0       5m37s&#x000A;pc-deployment-c848d76789   4         4         4       72s&#x000A;```&#x000A;&#x000A;##### 6.3.3 版本回退&#x000A;&#x000A;deployment支持版本升级过程中的暂停、继续功能以及版本回退等诸多功能，下面具体来看.&#x000A;&#x000A;kubectl rollout： 版本升级相关功能，支持下面的选项：&#x000A;&#x000A;- status	显示当前升级状态&#x000A;- history   显示 升级历史记录&#x000A;- pause    暂停版本升级过程&#x000A;- resume   继续已经暂停的版本升级过程&#x000A;- restart    重启版本升级过程&#x000A;- undo 回滚到上一级版本（可以使用--to-revision回滚到指定版本）&#x000A;&#x000A;```shell&#x000A;# 查看当前升级版本的状态&#x000A;[root@k8s-master01 ~]# kubectl rollout status deploy pc-deployment -n dev&#x000A;deployment &quot;pc-deployment&quot; successfully rolled out&#x000A;&#x000A;# 查看升级历史记录&#x000A;[root@k8s-master01 ~]# kubectl rollout history deploy pc-deployment -n dev&#x000A;deployment.apps/pc-deployment&#x000A;REVISION  CHANGE-CAUSE&#x000A;1         kubectl create --filename=pc-deployment.yaml --record=true&#x000A;2         kubectl create --filename=pc-deployment.yaml --record=true&#x000A;3         kubectl create --filename=pc-deployment.yaml --record=true&#x000A;# 可以发现有三次版本记录，说明完成过两次升级&#x000A;&#x000A;# 版本回滚&#x000A;# 这里直接使用--to-revision=1回滚到了1版本， 如果省略这个选项，就是回退到上个版本，就是2版本&#x000A;[root@k8s-master01 ~]# kubectl rollout undo deployment pc-deployment --to-revision=1 -n dev&#x000A;deployment.apps/pc-deployment rolled back&#x000A;&#x000A;# 查看发现，通过nginx镜像版本可以发现到了第一版&#x000A;[root@k8s-master01 ~]# kubectl get deploy -n dev -o wide&#x000A;NAME            READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES         &#x000A;pc-deployment   4/4     4            4           74m   nginx        nginx:1.17.1   &#x000A;&#x000A;# 查看rs，发现第一个rs中有4个pod运行，后面两个版本的rs中pod为运行&#x000A;# 其实deployment之所以可是实现版本的回滚，就是通过记录下历史rs来实现的，&#x000A;# 一旦想回滚到哪个版本，只需要将当前版本pod数量降为0，然后将回滚版本的pod提升为目标数量就可以了&#x000A;[root@k8s-master01 ~]# kubectl get rs -n dev&#x000A;NAME                       DESIRED   CURRENT   READY   AGE&#x000A;pc-deployment-6696798b78   4         4         4       78m&#x000A;pc-deployment-966bf7f44    0         0         0       37m&#x000A;pc-deployment-c848d767     0         0         0       71m&#x000A;```&#x000A;&#x000A;##### 6.3.4 金丝雀发布&#x000A;&#x000A;Deployment控制器支持控制更新过程中的控制，如“暂停(pause)”或“继续(resume)”更新操作。&#x000A;&#x000A;比如有一批新的Pod资源创建完成后立即暂停更新过程，此时，仅存在一部分新版本的应用，主体部分还是旧的版本。然后，再筛选一小部分的用户请求路由到新版本的Pod应用，继续观察能否稳定地按期望的方式运行。确定没问题之后再继续完成余下的Pod资源滚动更新，否则立即回滚更新操作。这就是所谓的金丝雀发布。&#x000A;&#x000A;```shell&#x000A;# 更新deployment的版本，并配置暂停deployment&#x000A;[root@k8s-master01 ~]#  kubectl set image deploy pc-deployment nginx=nginx:1.17.4 -n dev &amp;&amp; kubectl rollout pause deployment pc-deployment  -n dev&#x000A;deployment.apps/pc-deployment image updated&#x000A;deployment.apps/pc-deployment paused&#x000A;&#x000A;#观察更新状态&#x000A;[root@k8s-master01 ~]# kubectl rollout status deploy pc-deployment -n dev　&#x000A;Waiting for deployment &quot;pc-deployment&quot; rollout to finish: 2 out of 4 new replicas have been updated...&#x000A;&#x000A;# 监控更新的过程，可以看到已经新增了一个资源，但是并未按照预期的状态去删除一个旧的资源，就是因为使用了pause暂停命令&#x000A;&#x000A;[root@k8s-master01 ~]# kubectl get rs -n dev -o wide&#x000A;NAME                       DESIRED   CURRENT   READY   AGE     CONTAINERS   IMAGES         &#x000A;pc-deployment-5d89bdfbf9   3         3         3       19m     nginx        nginx:1.17.1   &#x000A;pc-deployment-675d469f8b   0         0         0       14m     nginx        nginx:1.17.2   &#x000A;pc-deployment-6c9f56fcfb   2         2         2       3m16s   nginx        nginx:1.17.4   &#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev&#x000A;NAME                             READY   STATUS    RESTARTS   AGE&#x000A;pc-deployment-5d89bdfbf9-rj8sq   1/1     Running   0          7m33s&#x000A;pc-deployment-5d89bdfbf9-ttwgg   1/1     Running   0          7m35s&#x000A;pc-deployment-5d89bdfbf9-v4wvc   1/1     Running   0          7m34s&#x000A;pc-deployment-6c9f56fcfb-996rt   1/1     Running   0          3m31s&#x000A;pc-deployment-6c9f56fcfb-j2gtj   1/1     Running   0          3m31s&#x000A;&#x000A;# 确保更新的pod没问题了，继续更新&#x000A;[root@k8s-master01 ~]# kubectl rollout resume deploy pc-deployment -n dev&#x000A;deployment.apps/pc-deployment resumed&#x000A;&#x000A;# 查看最后的更新情况&#x000A;[root@k8s-master01 ~]# kubectl get rs -n dev -o wide&#x000A;NAME                       DESIRED   CURRENT   READY   AGE     CONTAINERS   IMAGES         &#x000A;pc-deployment-5d89bdfbf9   0         0         0       21m     nginx        nginx:1.17.1   &#x000A;pc-deployment-675d469f8b   0         0         0       16m     nginx        nginx:1.17.2   &#x000A;pc-deployment-6c9f56fcfb   4         4         4       5m11s   nginx        nginx:1.17.4   &#x000A;&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev&#x000A;NAME                             READY   STATUS    RESTARTS   AGE&#x000A;pc-deployment-6c9f56fcfb-7bfwh   1/1     Running   0          37s&#x000A;pc-deployment-6c9f56fcfb-996rt   1/1     Running   0          5m27s&#x000A;pc-deployment-6c9f56fcfb-j2gtj   1/1     Running   0          5m27s&#x000A;pc-deployment-6c9f56fcfb-rf84v   1/1     Running   0          37s&#x000A;```&#x000A;&#x000A;**删除Deployment**&#x000A;&#x000A;```shell&#x000A;# 删除deployment，其下的rs和pod也将被删除&#x000A;[root@k8s-master01 ~]# kubectl delete -f pc-deployment.yaml&#x000A;deployment.apps &quot;pc-deployment&quot; deleted&#x000A;```&#x000A;&#x000A;#### 6.4 Horizontal Pod Autoscaler(HPA)&#x000A;&#x000A;在前面的课程中，我们已经可以实现通过手工执行`kubectl scale`命令实现Pod扩容或缩容，但是这显然不符合Kubernetes的定位目标--自动化、智能化。 Kubernetes期望可以实现通过监测Pod的使用情况，实现pod数量的自动调整，于是就产生了Horizontal Pod Autoscaler（HPA）这种控制器。&#x000A;&#x000A;HPA可以获取每个Pod利用率，然后和HPA中定义的指标进行对比，同时计算出需要伸缩的具体值，最后实现Pod的数量的调整。其实HPA与之前的Deployment一样，也属于一种Kubernetes资源对象，它通过追踪分析RC控制的所有目标Pod的负载变化情况，来确定是否需要针对性地调整目标Pod的副本数，这是HPA的实现原理。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200608155858271.png)&#x000A;&#x000A;接下来，我们来做一个实验&#x000A;&#x000A;##### 6.4.1 安装metrics-server&#x000A;&#x000A;metrics-server可以用来收集集群中的资源使用情况&#x000A;&#x000A;```shell&#x000A;# 安装git&#x000A;[root@k8s-master01 ~]# yum install git -y&#x000A;# 获取metrics-server, 注意使用的版本&#x000A;[root@k8s-master01 ~]# git clone -b v0.3.6 https://github.com/kubernetes-incubator/metrics-server&#x000A;# 修改deployment, 注意修改的是镜像和初始化参数&#x000A;[root@k8s-master01 ~]# cd /root/metrics-server/deploy/1.8+/&#x000A;[root@k8s-master01 1.8+]# vim metrics-server-deployment.yaml&#x000A;按图中添加下面选项&#x000A;hostNetwork: true&#x000A;image: registry.cn-hangzhou.aliyuncs.com/google_containers/metrics-server-amd64:v0.3.6&#x000A;args:&#x000A;- --kubelet-insecure-tls&#x000A;- --kubelet-preferred-address-types=InternalIP,Hostname,InternalDNS,ExternalDNS,ExternalIP&#x000A;```&#x000A;&#x000A;![image-20200608163326496](Kubenetes.assets/image-20200608163326496.png)&#x000A;&#x000A;```shell&#x000A;# 安装metrics-server&#x000A;[root@k8s-master01 1.8+]# kubectl apply -f ./&#x000A;&#x000A;# 查看pod运行情况&#x000A;[root@k8s-master01 1.8+]# kubectl get pod -n kube-system&#x000A;metrics-server-6b976979db-2xwbj   1/1     Running   0          90s&#x000A;&#x000A;# 使用kubectl top node 查看资源使用情况&#x000A;[root@k8s-master01 1.8+]# kubectl top node&#x000A;NAME           CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%&#x000A;k8s-master01   289m         14%    1582Mi          54%       &#x000A;k8s-node01     81m          4%     1195Mi          40%       &#x000A;k8s-node02     72m          3%     1211Mi          41%  &#x000A;[root@k8s-master01 1.8+]# kubectl top pod -n kube-system&#x000A;NAME                              CPU(cores)   MEMORY(bytes)&#x000A;coredns-6955765f44-7ptsb          3m           9Mi&#x000A;coredns-6955765f44-vcwr5          3m           8Mi&#x000A;etcd-master                       14m          145Mi&#x000A;...&#x000A;# 至此,metrics-server安装完成&#x000A;```&#x000A;&#x000A;##### 6.4.2 准备deployment和servie&#x000A;&#x000A;创建pc-hpa-pod.yaml文件，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1&#x000A;kind: Deployment&#x000A;metadata:&#x000A;  name: nginx&#x000A;  namespace: dev&#x000A;spec:&#x000A;  strategy: # 策略&#x000A;    type: RollingUpdate # 滚动更新策略&#x000A;  replicas: 1&#x000A;  selector:&#x000A;    matchLabels:&#x000A;      app: nginx-pod&#x000A;  template:&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: nginx-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: nginx&#x000A;        image: nginx:1.17.1&#x000A;        resources: # 资源配额&#x000A;          limits:  # 限制资源（上限）&#x000A;            cpu: &quot;1&quot; # CPU限制，单位是core数&#x000A;          requests: # 请求资源（下限）&#x000A;            cpu: &quot;100m&quot;  # CPU限制，单位是core数&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建deployment&#x000A;[root@k8s-master01 1.8+]# kubectl run nginx --image=nginx:1.17.1 --requests=cpu=100m -n dev&#x000A;# 创建service&#x000A;[root@k8s-master01 1.8+]# kubectl expose deployment nginx --type=NodePort --port=80 -n dev&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 查看&#x000A;[root@k8s-master01 1.8+]# kubectl get deployment,pod,svc -n dev&#x000A;NAME                    READY   UP-TO-DATE   AVAILABLE   AGE&#x000A;deployment.apps/nginx   1/1     1            1           47s&#x000A;&#x000A;NAME                         READY   STATUS    RESTARTS   AGE&#x000A;pod/nginx-7df9756ccc-bh8dr   1/1     Running   0          47s&#x000A;&#x000A;NAME            TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE&#x000A;service/nginx   NodePort   10.101.18.29   &lt;none&gt;        80:31830/TCP   35s&#x000A;```&#x000A;&#x000A;##### 6.4.3 部署HPA&#x000A;&#x000A;创建pc-hpa.yaml文件，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: autoscaling/v1&#x000A;kind: HorizontalPodAutoscaler&#x000A;metadata:&#x000A;  name: pc-hpa&#x000A;  namespace: dev&#x000A;spec:&#x000A;  minReplicas: 1  #最小pod数量&#x000A;  maxReplicas: 10 #最大pod数量&#x000A;  targetCPUUtilizationPercentage: 3 # CPU使用率指标&#x000A;  scaleTargetRef:   # 指定要控制的nginx信息&#x000A;    apiVersion:  apps/v1&#x000A;    kind: Deployment&#x000A;    name: nginx&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建hpa&#x000A;[root@k8s-master01 1.8+]# kubectl create -f pc-hpa.yaml&#x000A;horizontalpodautoscaler.autoscaling/pc-hpa created&#x000A;&#x000A;# 查看hpa&#x000A;    [root@k8s-master01 1.8+]# kubectl get hpa -n dev&#x000A;NAME     REFERENCE          TARGETS   MINPODS   MAXPODS   REPLICAS   AGE&#x000A;pc-hpa   Deployment/nginx   0%/3%     1         10        1          62s&#x000A;```&#x000A;&#x000A;##### 6.4.4 测试&#x000A;&#x000A;使用压测工具对service地址`192.168.5.4:31830`进行压测，然后通过控制台查看hpa和pod的变化&#x000A;&#x000A;hpa变化&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# kubectl get hpa -n dev -w&#x000A;NAME   REFERENCE      TARGETS  MINPODS  MAXPODS  REPLICAS  AGE&#x000A;pc-hpa  Deployment/nginx  0%/3%   1     10     1      4m11s&#x000A;pc-hpa  Deployment/nginx  0%/3%   1     10     1      5m19s&#x000A;pc-hpa  Deployment/nginx  22%/3%   1     10     1      6m50s&#x000A;pc-hpa  Deployment/nginx  22%/3%   1     10     4      7m5s&#x000A;pc-hpa  Deployment/nginx  22%/3%   1     10     8      7m21s&#x000A;pc-hpa  Deployment/nginx  6%/3%   1     10     8      7m51s&#x000A;pc-hpa  Deployment/nginx  0%/3%   1     10     8      9m6s&#x000A;pc-hpa  Deployment/nginx  0%/3%   1     10     8      13m&#x000A;pc-hpa  Deployment/nginx  0%/3%   1     10     1      14m&#x000A;```&#x000A;&#x000A;deployment变化&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# kubectl get deployment -n dev -w&#x000A;NAME    READY   UP-TO-DATE   AVAILABLE   AGE&#x000A;nginx   1/1     1            1           11m&#x000A;nginx   1/4     1            1           13m&#x000A;nginx   1/4     1            1           13m&#x000A;nginx   1/4     1            1           13m&#x000A;nginx   1/4     4            1           13m&#x000A;nginx   1/8     4            1           14m&#x000A;nginx   1/8     4            1           14m&#x000A;nginx   1/8     4            1           14m&#x000A;nginx   1/8     8            1           14m&#x000A;nginx   2/8     8            2           14m&#x000A;nginx   3/8     8            3           14m&#x000A;nginx   4/8     8            4           14m&#x000A;nginx   5/8     8            5           14m&#x000A;nginx   6/8     8            6           14m&#x000A;nginx   7/8     8            7           14m&#x000A;nginx   8/8     8            8           15m&#x000A;nginx   8/1     8            8           20m&#x000A;nginx   8/1     8            8           20m&#x000A;nginx   1/1     1            1           20m&#x000A;```&#x000A;&#x000A;pod变化&#x000A;&#x000A;```&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -w&#x000A;NAME                     READY   STATUS    RESTARTS   AGE&#x000A;nginx-7df9756ccc-bh8dr   1/1     Running   0          11m&#x000A;nginx-7df9756ccc-cpgrv   0/1     Pending   0          0s&#x000A;nginx-7df9756ccc-8zhwk   0/1     Pending   0          0s&#x000A;nginx-7df9756ccc-rr9bn   0/1     Pending   0          0s&#x000A;nginx-7df9756ccc-cpgrv   0/1     ContainerCreating   0          0s&#x000A;nginx-7df9756ccc-8zhwk   0/1     ContainerCreating   0          0s&#x000A;nginx-7df9756ccc-rr9bn   0/1     ContainerCreating   0          0s&#x000A;nginx-7df9756ccc-m9gsj   0/1     Pending             0          0s&#x000A;nginx-7df9756ccc-g56qb   0/1     Pending             0          0s&#x000A;nginx-7df9756ccc-sl9c6   0/1     Pending             0          0s&#x000A;nginx-7df9756ccc-fgst7   0/1     Pending             0          0s&#x000A;nginx-7df9756ccc-g56qb   0/1     ContainerCreating   0          0s&#x000A;nginx-7df9756ccc-m9gsj   0/1     ContainerCreating   0          0s&#x000A;nginx-7df9756ccc-sl9c6   0/1     ContainerCreating   0          0s&#x000A;nginx-7df9756ccc-fgst7   0/1     ContainerCreating   0          0s&#x000A;nginx-7df9756ccc-8zhwk   1/1     Running             0          19s&#x000A;nginx-7df9756ccc-rr9bn   1/1     Running             0          30s&#x000A;nginx-7df9756ccc-m9gsj   1/1     Running             0          21s&#x000A;nginx-7df9756ccc-cpgrv   1/1     Running             0          47s&#x000A;nginx-7df9756ccc-sl9c6   1/1     Running             0          33s&#x000A;nginx-7df9756ccc-g56qb   1/1     Running             0          48s&#x000A;nginx-7df9756ccc-fgst7   1/1     Running             0          66s&#x000A;nginx-7df9756ccc-fgst7   1/1     Terminating         0          6m50s&#x000A;nginx-7df9756ccc-8zhwk   1/1     Terminating         0          7m5s&#x000A;nginx-7df9756ccc-cpgrv   1/1     Terminating         0          7m5s&#x000A;nginx-7df9756ccc-g56qb   1/1     Terminating         0          6m50s&#x000A;nginx-7df9756ccc-rr9bn   1/1     Terminating         0          7m5s&#x000A;nginx-7df9756ccc-m9gsj   1/1     Terminating         0          6m50s&#x000A;nginx-7df9756ccc-sl9c6   1/1     Terminating         0          6m50s&#x000A;```&#x000A;&#x000A;#### 6.5 DaemonSet(DS)&#x000A;&#x000A;DaemonSet类型的控制器可以保证在集群中的每一台（或指定）节点上都运行一个副本。一般适用于日志收集、节点监控等场景。也就是说，如果一个Pod提供的功能是节点级别的（每个节点都需要且只需要一个），那么这类Pod就适合使用DaemonSet类型的控制器创建。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200612010223537.png)&#x000A;&#x000A;DaemonSet控制器的特点：&#x000A;&#x000A;- 每当向集群中添加一个节点时，指定的 Pod 副本也将添加到该节点上&#x000A;- 当节点从集群中移除时，Pod 也就被垃圾回收了&#x000A;&#x000A;下面先来看下DaemonSet的资源清单文件&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1 # 版本号&#x000A;kind: DaemonSet # 类型       &#x000A;metadata: # 元数据&#x000A;  name: # rs名称 &#x000A;  namespace: # 所属命名空间 &#x000A;  labels: #标签&#x000A;    controller: daemonset&#x000A;spec: # 详情描述&#x000A;  revisionHistoryLimit: 3 # 保留历史版本&#x000A;  updateStrategy: # 更新策略&#x000A;    type: RollingUpdate # 滚动更新策略&#x000A;    rollingUpdate: # 滚动更新&#x000A;      maxUnavailable: 1 # 最大不可用状态的 Pod 的最大值，可以为百分比，也可以为整数&#x000A;  selector: # 选择器，通过它指定该控制器管理哪些pod&#x000A;    matchLabels:      # Labels匹配规则&#x000A;      app: nginx-pod&#x000A;    matchExpressions: # Expressions匹配规则&#x000A;      - {key: app, operator: In, values: [nginx-pod]}&#x000A;  template: # 模板，当副本数量不足时，会根据下面的模板创建pod副本&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: nginx-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: nginx&#x000A;        image: nginx:1.17.1&#x000A;        ports:&#x000A;        - containerPort: 80&#x000A;```&#x000A;&#x000A;创建pc-daemonset.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1&#x000A;kind: DaemonSet      &#x000A;metadata:&#x000A;  name: pc-daemonset&#x000A;  namespace: dev&#x000A;spec: &#x000A;  selector:&#x000A;    matchLabels:&#x000A;      app: nginx-pod&#x000A;  template:&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: nginx-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: nginx&#x000A;        image: nginx:1.17.1&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建daemonset&#x000A;[root@k8s-master01 ~]# kubectl create -f  pc-daemonset.yaml&#x000A;daemonset.apps/pc-daemonset created&#x000A;&#x000A;# 查看daemonset&#x000A;[root@k8s-master01 ~]#  kubectl get ds -n dev -o wide&#x000A;NAME        DESIRED  CURRENT  READY  UP-TO-DATE  AVAILABLE   AGE   CONTAINERS   IMAGES         &#x000A;pc-daemonset   2        2        2      2           2        24s   nginx        nginx:1.17.1   &#x000A;&#x000A;# 查看pod,发现在每个Node上都运行一个pod&#x000A;[root@k8s-master01 ~]#  kubectl get pods -n dev -o wide&#x000A;NAME                 READY   STATUS    RESTARTS   AGE   IP            NODE    &#x000A;pc-daemonset-9bck8   1/1     Running   0          37s   10.244.1.43   node1     &#x000A;pc-daemonset-k224w   1/1     Running   0          37s   10.244.2.74   node2      &#x000A;&#x000A;# 删除daemonset&#x000A;[root@k8s-master01 ~]# kubectl delete -f pc-daemonset.yaml&#x000A;daemonset.apps &quot;pc-daemonset&quot; deleted&#x000A;```&#x000A;&#x000A;#### 6.6 Job&#x000A;&#x000A;Job，主要用于负责**批量处理(一次要处理指定数量任务)**短暂的**一次性(每个任务仅运行一次就结束)**任务。Job特点如下：&#x000A;&#x000A;- 当Job创建的pod执行成功结束时，Job将记录成功结束的pod数量&#x000A;- 当成功结束的pod达到指定的数量时，Job将完成执行&#x000A;&#x000A;![img](Kubenetes.assets/image-20200618213054113.png)&#x000A;&#x000A;Job的资源清单文件：&#x000A;&#x000A;&#x000A;&#x000A;```yaml&#x000A;apiVersion: batch/v1 # 版本号&#x000A;kind: Job # 类型       &#x000A;metadata: # 元数据&#x000A;  name: # rs名称 &#x000A;  namespace: # 所属命名空间 &#x000A;  labels: #标签&#x000A;    controller: job&#x000A;spec: # 详情描述&#x000A;  completions: 1 # 指定job需要成功运行Pods的次数。默认值: 1&#x000A;  parallelism: 1 # 指定job在任一时刻应该并发运行Pods的数量。默认值: 1&#x000A;  activeDeadlineSeconds: 30 # 指定job可运行的时间期限，超过时间还未结束，系统将会尝试进行终止。&#x000A;  backoffLimit: 6 # 指定job失败后进行重试的次数。默认是6&#x000A;  manualSelector: true # 是否可以使用selector选择器选择pod，默认是false&#x000A;  selector: # 选择器，通过它指定该控制器管理哪些pod&#x000A;    matchLabels:      # Labels匹配规则&#x000A;      app: counter-pod&#x000A;    matchExpressions: # Expressions匹配规则&#x000A;      - {key: app, operator: In, values: [counter-pod]}&#x000A;  template: # 模板，当副本数量不足时，会根据下面的模板创建pod副本&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: counter-pod&#x000A;    spec:&#x000A;      restartPolicy: Never # 重启策略只能设置为Never或者OnFailure&#x000A;      containers:&#x000A;      - name: counter&#x000A;        image: busybox:1.30&#x000A;        command: [&quot;bin/sh&quot;,&quot;-c&quot;,&quot;for i in 9 8 7 6 5 4 3 2 1; do echo $i;sleep 2;done&quot;]&#x000A;```&#x000A;&#x000A;```markdown&#x000A;关于重启策略设置的说明：&#x000A;    如果指定为OnFailure，则job会在pod出现故障时重启容器，而不是创建pod，failed次数不变&#x000A;    如果指定为Never，则job会在pod出现故障时创建新的pod，并且故障pod不会消失，也不会重启，failed次数加1&#x000A;    如果指定为Always的话，就意味着一直重启，意味着job任务会重复去执行了，当然不对，所以不能设置为Always&#x000A;```&#x000A;&#x000A;创建pc-job.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: batch/v1&#x000A;kind: Job      &#x000A;metadata:&#x000A;  name: pc-job&#x000A;  namespace: dev&#x000A;spec:&#x000A;  manualSelector: true&#x000A;  selector:&#x000A;    matchLabels:&#x000A;      app: counter-pod&#x000A;  template:&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: counter-pod&#x000A;    spec:&#x000A;      restartPolicy: Never&#x000A;      containers:&#x000A;      - name: counter&#x000A;        image: busybox:1.30&#x000A;        command: [&quot;bin/sh&quot;,&quot;-c&quot;,&quot;for i in 9 8 7 6 5 4 3 2 1; do echo $i;sleep 3;done&quot;]&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建job&#x000A;[root@k8s-master01 ~]# kubectl create -f pc-job.yaml&#x000A;job.batch/pc-job created&#x000A;&#x000A;# 查看job&#x000A;[root@k8s-master01 ~]# kubectl get job -n dev -o wide  -w&#x000A;NAME     COMPLETIONS   DURATION   AGE   CONTAINERS   IMAGES         SELECTOR&#x000A;pc-job   0/1           21s        21s   counter      busybox:1.30   app=counter-pod&#x000A;pc-job   1/1           31s        79s   counter      busybox:1.30   app=counter-pod&#x000A;&#x000A;# 通过观察pod状态可以看到，pod在运行完毕任务后，就会变成Completed状态&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -w&#x000A;NAME           READY   STATUS     RESTARTS      AGE&#x000A;pc-job-rxg96   1/1     Running     0            29s&#x000A;pc-job-rxg96   0/1     Completed   0            33s&#x000A;&#x000A;# 接下来，调整下pod运行的总数量和并行数量 即：在spec下设置下面两个选项&#x000A;#  completions: 6 # 指定job需要成功运行Pods的次数为6&#x000A;#  parallelism: 3 # 指定job并发运行Pods的数量为3&#x000A;#  然后重新运行job，观察效果，此时会发现，job会每次运行3个pod，总共执行了6个pod&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -w&#x000A;NAME           READY   STATUS    RESTARTS   AGE&#x000A;pc-job-684ft   1/1     Running   0          5s&#x000A;pc-job-jhj49   1/1     Running   0          5s&#x000A;pc-job-pfcvh   1/1     Running   0          5s&#x000A;pc-job-684ft   0/1     Completed   0          11s&#x000A;pc-job-v7rhr   0/1     Pending     0          0s&#x000A;pc-job-v7rhr   0/1     Pending     0          0s&#x000A;pc-job-v7rhr   0/1     ContainerCreating   0          0s&#x000A;pc-job-jhj49   0/1     Completed           0          11s&#x000A;pc-job-fhwf7   0/1     Pending             0          0s&#x000A;pc-job-fhwf7   0/1     Pending             0          0s&#x000A;pc-job-pfcvh   0/1     Completed           0          11s&#x000A;pc-job-5vg2j   0/1     Pending             0          0s&#x000A;pc-job-fhwf7   0/1     ContainerCreating   0          0s&#x000A;pc-job-5vg2j   0/1     Pending             0          0s&#x000A;pc-job-5vg2j   0/1     ContainerCreating   0          0s&#x000A;pc-job-fhwf7   1/1     Running             0          2s&#x000A;pc-job-v7rhr   1/1     Running             0          2s&#x000A;pc-job-5vg2j   1/1     Running             0          3s&#x000A;pc-job-fhwf7   0/1     Completed           0          12s&#x000A;pc-job-v7rhr   0/1     Completed           0          12s&#x000A;pc-job-5vg2j   0/1     Completed           0          12s&#x000A;&#x000A;# 删除job&#x000A;[root@k8s-master01 ~]# kubectl delete -f pc-job.yaml&#x000A;job.batch &quot;pc-job&quot; deleted&#x000A;```&#x000A;&#x000A;#### 6.7 CronJob(CJ)&#x000A;&#x000A;CronJob控制器以 Job控制器资源为其管控对象，并借助它管理pod资源对象，Job控制器定义的作业任务在其控制器资源创建之后便会立即执行，但CronJob可以以类似于Linux操作系统的周期性任务作业计划的方式控制其运行**时间点**及**重复运行**的方式。也就是说，**CronJob可以在特定的时间点(反复的)去运行job任务**。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200618213149531.png)&#x000A;&#x000A;CronJob的资源清单文件：&#x000A;&#x000A;```yaml&#x000A;apiVersion: batch/v1beta1 # 版本号&#x000A;kind: CronJob # 类型       &#x000A;metadata: # 元数据&#x000A;  name: # rs名称 &#x000A;  namespace: # 所属命名空间 &#x000A;  labels: #标签&#x000A;    controller: cronjob&#x000A;spec: # 详情描述&#x000A;  schedule: # cron格式的作业调度运行时间点,用于控制任务在什么时间执行&#x000A;  concurrencyPolicy: # 并发执行策略，用于定义前一次作业运行尚未完成时是否以及如何运行后一次的作业&#x000A;  failedJobHistoryLimit: # 为失败的任务执行保留的历史记录数，默认为1&#x000A;  successfulJobHistoryLimit: # 为成功的任务执行保留的历史记录数，默认为3&#x000A;  startingDeadlineSeconds: # 启动作业错误的超时时长&#x000A;  jobTemplate: # job控制器模板，用于为cronjob控制器生成job对象;下面其实就是job的定义&#x000A;    metadata:&#x000A;    spec:&#x000A;      completions: 1&#x000A;      parallelism: 1&#x000A;      activeDeadlineSeconds: 30&#x000A;      backoffLimit: 6&#x000A;      manualSelector: true&#x000A;      selector:&#x000A;        matchLabels:&#x000A;          app: counter-pod&#x000A;        matchExpressions: 规则&#x000A;          - {key: app, operator: In, values: [counter-pod]}&#x000A;      template:&#x000A;        metadata:&#x000A;          labels:&#x000A;            app: counter-pod&#x000A;        spec:&#x000A;          restartPolicy: Never &#x000A;          containers:&#x000A;          - name: counter&#x000A;            image: busybox:1.30&#x000A;            command: [&quot;bin/sh&quot;,&quot;-c&quot;,&quot;for i in 9 8 7 6 5 4 3 2 1; do echo $i;sleep 20;done&quot;]&#x000A;```&#x000A;&#x000A;```markdown&#x000A;需要重点解释的几个选项：&#x000A;schedule: cron表达式，用于指定任务的执行时间&#x000A;    */1    *      *    *     *&#x000A;    &lt;分钟&gt; &lt;小时&gt; &lt;日&gt; &lt;月份&gt; &lt;星期&gt;&#x000A;&#x000A;    分钟 值从 0 到 59.&#x000A;    小时 值从 0 到 23.&#x000A;    日 值从 1 到 31.&#x000A;    月 值从 1 到 12.&#x000A;    星期 值从 0 到 6, 0 代表星期日&#x000A;    多个时间可以用逗号隔开； 范围可以用连字符给出；*可以作为通配符； /表示每...&#x000A;concurrencyPolicy:&#x000A;    Allow:   允许Jobs并发运行(默认)&#x000A;    Forbid:  禁止并发运行，如果上一次运行尚未完成，则跳过下一次运行&#x000A;    Replace: 替换，取消当前正在运行的作业并用新作业替换它&#x000A;```&#x000A;&#x000A;创建pc-cronjob.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: batch/v1beta1&#x000A;kind: CronJob&#x000A;metadata:&#x000A;  name: pc-cronjob&#x000A;  namespace: dev&#x000A;  labels:&#x000A;    controller: cronjob&#x000A;spec:&#x000A;  schedule: &quot;*/1 * * * *&quot;&#x000A;  jobTemplate:&#x000A;    metadata:&#x000A;    spec:&#x000A;      template:&#x000A;        spec:&#x000A;          restartPolicy: Never&#x000A;          containers:&#x000A;          - name: counter&#x000A;            image: busybox:1.30&#x000A;            command: [&quot;bin/sh&quot;,&quot;-c&quot;,&quot;for i in 9 8 7 6 5 4 3 2 1; do echo $i;sleep 3;done&quot;]&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建cronjob&#x000A;[root@k8s-master01 ~]# kubectl create -f pc-cronjob.yaml&#x000A;cronjob.batch/pc-cronjob created&#x000A;&#x000A;# 查看cronjob&#x000A;[root@k8s-master01 ~]# kubectl get cronjobs -n dev&#x000A;NAME         SCHEDULE      SUSPEND   ACTIVE   LAST SCHEDULE   AGE&#x000A;pc-cronjob   */1 * * * *   False     0        &lt;none&gt;          6s&#x000A;&#x000A;# 查看job&#x000A;[root@k8s-master01 ~]# kubectl get jobs -n dev&#x000A;NAME                    COMPLETIONS   DURATION   AGE&#x000A;pc-cronjob-1592587800   1/1           28s        3m26s&#x000A;pc-cronjob-1592587860   1/1           28s        2m26s&#x000A;pc-cronjob-1592587920   1/1           28s        86s&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev&#x000A;pc-cronjob-1592587800-x4tsm   0/1     Completed   0          2m24s&#x000A;pc-cronjob-1592587860-r5gv4   0/1     Completed   0          84s&#x000A;pc-cronjob-1592587920-9dxxq   1/1     Running     0          24s&#x000A;&#x000A;&#x000A;# 删除cronjob&#x000A;[root@k8s-master01 ~]# kubectl  delete -f pc-cronjob.yaml&#x000A;cronjob.batch &quot;pc-cronjob&quot; deleted&#x000A;```&#x000A;&#x000A; &#x000A;&#x000A;### 7. Service详解&#x000A;&#x000A;#### 7.1 Service介绍&#x000A;&#x000A;在kubernetes中，pod是应用程序的载体，我们可以通过pod的ip来访问应用程序，但是pod的ip地址不是固定的，这也就意味着不方便直接采用pod的ip对服务进行访问。&#x000A;&#x000A;为了解决这个问题，kubernetes提供了Service资源，Service会对提供同一个服务的多个pod进行聚合，并且提供一个统一的入口地址。通过访问Service的入口地址就能访问到后面的pod服务。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200408194716912-1626783758946.png)&#x000A;&#x000A;Service在很多情况下只是一个概念，真正起作用的其实是kube-proxy服务进程，每个Node节点上都运行着一个kube-proxy服务进程。当创建Service的时候会通过api-server向etcd写入创建的service的信息，而kube-proxy会基于监听的机制发现这种Service的变动，然后**它会将最新的Service信息转换成对应的访问规则**。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200509121254425.png)&#x000A;&#x000A;&#x000A;&#x000A;```&#x000A;# 10.97.97.97:80 是service提供的访问入口&#x000A;# 当访问这个入口的时候，可以发现后面有三个pod的服务在等待调用，&#x000A;# kube-proxy会基于rr（轮询）的策略，将请求分发到其中一个pod上去&#x000A;# 这个规则会同时在集群内的所有节点上都生成，所以在任何一个节点上，都可以访问。&#x000A;[root@node1 ~]# ipvsadm -Ln&#x000A;IP Virtual Server version 1.2.1 (size=4096)&#x000A;Prot LocalAddress:Port Scheduler Flags&#x000A;  -&gt; RemoteAddress:Port           Forward Weight ActiveConn InActConn&#x000A;TCP  10.97.97.97:80 rr&#x000A;  -&gt; 10.244.1.39:80               Masq    1      0          0&#x000A;  -&gt; 10.244.1.40:80               Masq    1      0          0&#x000A;  -&gt; 10.244.2.33:80               Masq    1      0          0&#x000A;```&#x000A;&#x000A;kube-proxy目前支持三种工作模式:&#x000A;&#x000A;##### 7.1.1 userspace 模式&#x000A;&#x000A;userspace模式下，kube-proxy会为每一个Service创建一个监听端口，发向Cluster IP的请求被Iptables规则重定向到kube-proxy监听的端口上，kube-proxy根据LB算法选择一个提供服务的Pod并和其建立链接，以将请求转发到Pod上。  该模式下，kube-proxy充当了一个四层负责均衡器的角色。由于kube-proxy运行在userspace中，在进行转发处理时会增加内核和用户空间之间的数据拷贝，虽然比较稳定，但是效率比较低。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200509151424280.png)&#x000A;&#x000A;##### 7.1.2 iptables 模式&#x000A;&#x000A;iptables模式下，kube-proxy为service后端的每个Pod创建对应的iptables规则，直接将发向Cluster IP的请求重定向到一个Pod IP。  该模式下kube-proxy不承担四层负责均衡器的角色，只负责创建iptables规则。该模式的优点是较userspace模式效率更高，但不能提供灵活的LB策略，当后端Pod不可用时也无法进行重试。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200509152947714.png)&#x000A;&#x000A;##### 7.1.3 ipvs 模式&#x000A;&#x000A;ipvs模式和iptables类似，kube-proxy监控Pod的变化并创建相应的ipvs规则。ipvs相对iptables转发效率更高。除此以外，ipvs支持更多的LB算法。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200509153731363.png)&#x000A;&#x000A;```shell&#x000A;# 此模式必须安装ipvs内核模块，否则会降级为iptables&#x000A;# 开启ipvs&#x000A;[root@k8s-master01 ~]# kubectl edit cm kube-proxy -n kube-system&#x000A;# 修改mode: &quot;ipvs&quot;&#x000A;[root@k8s-master01 ~]# kubectl delete pod -l k8s-app=kube-proxy -n kube-system&#x000A;[root@node1 ~]# ipvsadm -Ln&#x000A;IP Virtual Server version 1.2.1 (size=4096)&#x000A;Prot LocalAddress:Port Scheduler Flags&#x000A;  -&gt; RemoteAddress:Port           Forward Weight ActiveConn InActConn&#x000A;TCP  10.97.97.97:80 rr&#x000A;  -&gt; 10.244.1.39:80               Masq    1      0          0&#x000A;  -&gt; 10.244.1.40:80               Masq    1      0          0&#x000A;  -&gt; 10.244.2.33:80               Masq    1      0          0&#x000A;```&#x000A;&#x000A;#### 7.2 Service类型&#x000A;&#x000A;Service的资源清单文件：&#x000A;&#x000A;```yaml&#x000A;kind: Service  # 资源类型&#x000A;apiVersion: v1  # 资源版本&#x000A;metadata: # 元数据&#x000A;  name: service # 资源名称&#x000A;  namespace: dev # 命名空间&#x000A;spec: # 描述&#x000A;  selector: # 标签选择器，用于确定当前service代理哪些pod&#x000A;    app: nginx&#x000A;  type: # Service类型，指定service的访问方式&#x000A;  clusterIP:  # 虚拟服务的ip地址&#x000A;  sessionAffinity: # session亲和性，支持ClientIP、None两个选项&#x000A;  ports: # 端口信息&#x000A;    - protocol: TCP &#x000A;      port: 3017  # service端口&#x000A;      targetPort: 5003 # pod端口&#x000A;      nodePort: 31122 # 主机端口&#x000A;```&#x000A;&#x000A;- ClusterIP：默认值，它是Kubernetes系统自动分配的虚拟IP，只能在集群内部访问&#x000A;- NodePort：将Service通过指定的Node上的端口暴露给外部，通过此方法，就可以在集群外部访问服务&#x000A;- LoadBalancer：使用外接负载均衡器完成到服务的负载分发，注意此模式需要外部云环境支持&#x000A;- ExternalName： 把集群外部的服务引入集群内部，直接使用&#x000A;&#x000A;#### 7.3 Service使用&#x000A;&#x000A;##### 7.3.1 实验环境准备&#x000A;&#x000A;在使用service之前，首先利用Deployment创建出3个pod，注意要为pod设置`app=nginx-pod`的标签&#x000A;&#x000A;创建deployment.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1&#x000A;kind: Deployment      &#x000A;metadata:&#x000A;  name: pc-deployment&#x000A;  namespace: dev&#x000A;spec: &#x000A;  replicas: 3&#x000A;  selector:&#x000A;    matchLabels:&#x000A;      app: nginx-pod&#x000A;  template:&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: nginx-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: nginx&#x000A;        image: nginx:1.17.1&#x000A;        ports:&#x000A;        - containerPort: 80&#x000A;```&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# kubectl create -f deployment.yaml&#x000A;deployment.apps/pc-deployment created&#x000A;&#x000A;# 查看pod详情&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -o wide --show-labels&#x000A;NAME                             READY   STATUS     IP            NODE     LABELS&#x000A;pc-deployment-66cb59b984-8p84h   1/1     Running    10.244.1.39   node1    app=nginx-pod&#x000A;pc-deployment-66cb59b984-vx8vx   1/1     Running    10.244.2.33   node2    app=nginx-pod&#x000A;pc-deployment-66cb59b984-wnncx   1/1     Running    10.244.1.40   node1    app=nginx-pod&#x000A;&#x000A;# 为了方便后面的测试，修改下三台nginx的index.html页面（三台修改的IP地址不一致）&#x000A;# kubectl exec -it pc-deployment-66cb59b984-8p84h -n dev /bin/sh&#x000A;# echo &quot;10.244.1.39&quot; &gt; /usr/share/nginx/html/index.html&#x000A;&#x000A;#修改完毕之后，访问测试&#x000A;[root@k8s-master01 ~]# curl 10.244.1.39&#x000A;10.244.1.39&#x000A;[root@k8s-master01 ~]# curl 10.244.2.33&#x000A;10.244.2.33&#x000A;[root@k8s-master01 ~]# curl 10.244.1.40&#x000A;10.244.1.40&#x000A;```&#x000A;&#x000A;##### 7.3.2 ClusterIP类型的Service&#x000A;&#x000A;创建service-clusterip.yaml文件&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Service&#x000A;metadata:&#x000A;  name: service-clusterip&#x000A;  namespace: dev&#x000A;spec:&#x000A;  selector:&#x000A;    app: nginx-pod&#x000A;  clusterIP: 10.97.97.97 # service的ip地址，如果不写，默认会生成一个&#x000A;  type: ClusterIP&#x000A;  ports:&#x000A;  - port: 80  # Service端口       &#x000A;    targetPort: 80 # pod端口&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建service&#x000A;[root@k8s-master01 ~]# kubectl create -f service-clusterip.yaml&#x000A;service/service-clusterip created&#x000A;&#x000A;# 查看service&#x000A;[root@k8s-master01 ~]# kubectl get svc -n dev -o wide&#x000A;NAME                TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)   AGE   SELECTOR&#x000A;service-clusterip   ClusterIP   10.97.97.97   &lt;none&gt;        80/TCP    13s   app=nginx-pod&#x000A;&#x000A;# 查看service的详细信息&#x000A;# 在这里有一个Endpoints列表，里面就是当前service可以负载到的服务入口&#x000A;[root@k8s-master01 ~]# kubectl describe svc service-clusterip -n dev&#x000A;Name:              service-clusterip&#x000A;Namespace:         dev&#x000A;Labels:            &lt;none&gt;&#x000A;Annotations:       &lt;none&gt;&#x000A;Selector:          app=nginx-pod&#x000A;Type:              ClusterIP&#x000A;IP:                10.97.97.97&#x000A;Port:              &lt;unset&gt;  80/TCP&#x000A;TargetPort:        80/TCP&#x000A;Endpoints:         10.244.1.39:80,10.244.1.40:80,10.244.2.33:80&#x000A;Session Affinity:  None&#x000A;Events:            &lt;none&gt;&#x000A;&#x000A;# 查看ipvs的映射规则&#x000A;[root@k8s-master01 ~]# ipvsadm -Ln&#x000A;TCP  10.97.97.97:80 rr&#x000A;  -&gt; 10.244.1.39:80               Masq    1      0          0&#x000A;  -&gt; 10.244.1.40:80               Masq    1      0          0&#x000A;  -&gt; 10.244.2.33:80               Masq    1      0          0&#x000A;&#x000A;# 访问10.97.97.97:80观察效果&#x000A;[root@k8s-master01 ~]# curl 10.97.97.97:80&#x000A;10.244.2.33&#x000A;```&#x000A;&#x000A;##### 7.3.3 Endpoint&#x000A;&#x000A;Endpoint是kubernetes中的一个资源对象，存储在etcd中，用来记录一个service对应的所有pod的访问地址，它是根据service配置文件中selector描述产生的。&#x000A;&#x000A;一个Service由一组Pod组成，这些Pod通过Endpoints暴露出来，**Endpoints是实现实际服务的端点集合**。换句话说，service和pod之间的联系是通过endpoints实现的。&#x000A;&#x000A;![image-20200509191917069](Kubenetes.assets/image-20200509191917069.png)&#x000A;&#x000A;**负载分发策略**&#x000A;&#x000A;对Service的访问被分发到了后端的Pod上去，目前kubernetes提供了两种负载分发策略：&#x000A;&#x000A;- 如果不定义，默认使用kube-proxy的策略，比如随机、轮询&#x000A;&#x000A;- 基于客户端地址的会话保持模式，即来自同一个客户端发起的所有请求都会转发到固定的一个Pod上&#x000A;&#x000A;  此模式可以使在spec中添加`sessionAffinity:ClientIP`选项&#x000A;&#x000A;```shell&#x000A;# 查看ipvs的映射规则【rr 轮询】&#x000A;[root@k8s-master01 ~]# ipvsadm -Ln&#x000A;TCP  10.97.97.97:80 rr&#x000A;  -&gt; 10.244.1.39:80               Masq    1      0          0&#x000A;  -&gt; 10.244.1.40:80               Masq    1      0          0&#x000A;  -&gt; 10.244.2.33:80               Masq    1      0          0&#x000A;&#x000A;# 循环访问测试&#x000A;[root@k8s-master01 ~]# while true;do curl 10.97.97.97:80; sleep 5; done;&#x000A;10.244.1.40&#x000A;10.244.1.39&#x000A;10.244.2.33&#x000A;10.244.1.40&#x000A;10.244.1.39&#x000A;10.244.2.33&#x000A;&#x000A;# 修改分发策略----sessionAffinity:ClientIP&#x000A;&#x000A;# 查看ipvs规则【persistent 代表持久】&#x000A;[root@k8s-master01 ~]# ipvsadm -Ln&#x000A;TCP  10.97.97.97:80 rr persistent 10800&#x000A;  -&gt; 10.244.1.39:80               Masq    1      0          0&#x000A;  -&gt; 10.244.1.40:80               Masq    1      0          0&#x000A;  -&gt; 10.244.2.33:80               Masq    1      0          0&#x000A;&#x000A;# 循环访问测试&#x000A;[root@k8s-master01 ~]# while true;do curl 10.97.97.97; sleep 5; done;&#x000A;10.244.2.33&#x000A;10.244.2.33&#x000A;10.244.2.33&#x000A;  &#x000A;# 删除service&#x000A;[root@k8s-master01 ~]# kubectl delete -f service-clusterip.yaml&#x000A;service &quot;service-clusterip&quot; deleted&#x000A;```&#x000A;&#x000A;##### 7.3.4 HeadLiness类型的Service&#x000A;&#x000A;在某些场景中，开发人员可能不想使用Service提供的负载均衡功能，而希望自己来控制负载均衡策略，针对这种情况，kubernetes提供了HeadLiness Service，这类Service不会分配Cluster IP，如果想要访问service，只能通过service的域名进行查询。&#x000A;&#x000A;创建service-headliness.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Service&#x000A;metadata:&#x000A;  name: service-headliness&#x000A;  namespace: dev&#x000A;spec:&#x000A;  selector:&#x000A;    app: nginx-pod&#x000A;  clusterIP: None # 将clusterIP设置为None，即可创建headliness Service&#x000A;  type: ClusterIP&#x000A;  ports:&#x000A;  - port: 80    &#x000A;    targetPort: 80&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建service&#x000A;[root@k8s-master01 ~]# kubectl create -f service-headliness.yaml&#x000A;service/service-headliness created&#x000A;&#x000A;# 获取service， 发现CLUSTER-IP未分配&#x000A;[root@k8s-master01 ~]# kubectl get svc service-headliness -n dev -o wide&#x000A;NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE   SELECTOR&#x000A;service-headliness   ClusterIP   None         &lt;none&gt;        80/TCP    11s   app=nginx-pod&#x000A;&#x000A;# 查看service详情&#x000A;[root@k8s-master01 ~]# kubectl describe svc service-headliness  -n dev&#x000A;Name:              service-headliness&#x000A;Namespace:         dev&#x000A;Labels:            &lt;none&gt;&#x000A;Annotations:       &lt;none&gt;&#x000A;Selector:          app=nginx-pod&#x000A;Type:              ClusterIP&#x000A;IP:                None&#x000A;Port:              &lt;unset&gt;  80/TCP&#x000A;TargetPort:        80/TCP&#x000A;Endpoints:         10.244.1.39:80,10.244.1.40:80,10.244.2.33:80&#x000A;Session Affinity:  None&#x000A;Events:            &lt;none&gt;&#x000A;&#x000A;# 查看域名的解析情况&#x000A;[root@k8s-master01 ~]# kubectl exec -it pc-deployment-66cb59b984-8p84h -n dev /bin/sh&#x000A;/ # cat /etc/resolv.conf&#x000A;nameserver 10.96.0.10&#x000A;search dev.svc.cluster.local svc.cluster.local cluster.local&#x000A;&#x000A;[root@k8s-master01 ~]# dig @10.96.0.10 service-headliness.dev.svc.cluster.local&#x000A;service-headliness.dev.svc.cluster.local. 30 IN A 10.244.1.40&#x000A;service-headliness.dev.svc.cluster.local. 30 IN A 10.244.1.39&#x000A;service-headliness.dev.svc.cluster.local. 30 IN A 10.244.2.33&#x000A;```&#x000A;&#x000A;##### 7.3.5 NodePort类型的Service&#x000A;&#x000A;在之前的样例中，创建的Service的ip地址只有集群内部才可以访问，如果希望将Service暴露给集群外部使用，那么就要使用到另外一种类型的Service，称为NodePort类型。NodePort的工作原理其实就是**将service的端口映射到Node的一个端口上**，然后就可以通过`NodeIp:NodePort`来访问service了。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200620175731338.png)&#x000A;&#x000A;创建service-nodeport.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Service&#x000A;metadata:&#x000A;  name: service-nodeport&#x000A;  namespace: dev&#x000A;spec:&#x000A;  selector:&#x000A;    app: nginx-pod&#x000A;  type: NodePort # service类型&#x000A;  ports:&#x000A;  - port: 80&#x000A;    nodePort: 30002 # 指定绑定的node的端口(默认的取值范围是：30000-32767), 如果不指定，会默认分配&#x000A;    targetPort: 80&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建service&#x000A;[root@k8s-master01 ~]# kubectl create -f service-nodeport.yaml&#x000A;service/service-nodeport created&#x000A;&#x000A;# 查看service&#x000A;[root@k8s-master01 ~]# kubectl get svc -n dev -o wide&#x000A;NAME               TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)       SELECTOR&#x000A;service-nodeport   NodePort   10.105.64.191   &lt;none&gt;        80:30002/TCP  app=nginx-pod&#x000A;&#x000A;# 接下来可以通过电脑主机的浏览器去访问集群中任意一个nodeip的30002端口，即可访问到pod&#x000A;```&#x000A;&#x000A;##### 7.3.6 LoadBalancer类型的Service&#x000A;&#x000A;LoadBalancer和NodePort很相似，目的都是向外部暴露一个端口，区别在于LoadBalancer会在集群的外部再来做一个负载均衡设备，而这个设备需要外部环境支持的，外部服务发送到这个设备上的请求，会被设备负载之后转发到集群中。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200510103945494.png)&#x000A;&#x000A;##### 7.3.7 ExternalName类型的Service&#x000A;&#x000A;ExternalName类型的Service用于引入集群外部的服务，它通过`externalName`属性指定外部一个服务的地址，然后在集群内部访问此service就可以访问到外部的服务了。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200510113311209.png)&#x000A;&#x000A;```shell&#x000A;apiVersion: v1&#x000A;kind: Service&#x000A;metadata:&#x000A;  name: service-externalname&#x000A;  namespace: dev&#x000A;spec:&#x000A;  type: ExternalName # service类型&#x000A;  externalName: www.baidu.com  #改成ip地址也可以&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建service&#x000A;[root@k8s-master01 ~]# kubectl  create -f service-externalname.yaml&#x000A;service/service-externalname created&#x000A;&#x000A;# 域名解析&#x000A;[root@k8s-master01 ~]# dig @10.96.0.10 service-externalname.dev.svc.cluster.local&#x000A;service-externalname.dev.svc.cluster.local. 30 IN CNAME www.baidu.com.&#x000A;www.baidu.com.          30      IN      CNAME   www.a.shifen.com.&#x000A;www.a.shifen.com.       30      IN      A       39.156.66.18&#x000A;www.a.shifen.com.       30      IN      A       39.156.66.14&#x000A;```&#x000A;&#x000A;#### 7.4 Ingress介绍&#x000A;&#x000A;在前面课程中已经提到，Service对集群之外暴露服务的主要方式有两种：NotePort和LoadBalancer，但是这两种方式，都有一定的缺点：&#x000A;&#x000A;- NodePort方式的缺点是会占用很多集群机器的端口，那么当集群服务变多的时候，这个缺点就愈发明显&#x000A;- LB方式的缺点是每个service需要一个LB，浪费、麻烦，并且需要kubernetes之外设备的支持&#x000A;&#x000A;基于这种现状，kubernetes提供了Ingress资源对象，Ingress只需要一个NodePort或者一个LB就可以满足暴露多个Service的需求。工作机制大致如下图表示：&#x000A;&#x000A;![img](Kubenetes.assets/image-20200623092808049.png)&#x000A;&#x000A;实际上，Ingress相当于一个7层的负载均衡器，是kubernetes对反向代理的一个抽象，它的工作原理类似于Nginx，可以理解成在**Ingress里建立诸多映射规则，Ingress Controller通过监听这些配置规则并转化成Nginx的反向代理配置 , 然后对外部提供服务**。在这里有两个核心概念：&#x000A;&#x000A;- ingress：kubernetes中的一个对象，作用是定义请求如何转发到service的规则&#x000A;- ingress controller：具体实现反向代理及负载均衡的程序，对ingress定义的规则进行解析，根据配置的规则来实现请求转发，实现方式有很多，比如Nginx, Contour, Haproxy等等&#x000A;&#x000A;Ingress（以Nginx为例）的工作原理如下：&#x000A;&#x000A;1. 用户编写Ingress规则，说明哪个域名对应kubernetes集群中的哪个Service&#x000A;2. Ingress控制器动态感知Ingress服务规则的变化，然后生成一段对应的Nginx反向代理配置&#x000A;3. Ingress控制器会将生成的Nginx配置写入到一个运行着的Nginx服务中，并动态更新&#x000A;4. 到此为止，其实真正在工作的就是一个Nginx了，内部配置了用户定义的请求转发规则&#x000A;&#x000A;![img](Kubenetes.assets/image-20200516112704764.png)&#x000A;&#x000A;#### 7.5 Ingress使用&#x000A;&#x000A;##### 7.5.1 环境准备 搭建ingress环境&#x000A;&#x000A;```makefile&#x000A;# 创建文件夹&#x000A;[root@k8s-master01 ~]# mkdir ingress-controller&#x000A;[root@k8s-master01 ~]# cd ingress-controller/&#x000A;&#x000A;# 获取ingress-nginx，本次案例使用的是0.30版本&#x000A;[root@k8s-master01 ingress-controller]# wget https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.30.0/deploy/static/mandatory.yaml&#x000A;[root@k8s-master01 ingress-controller]# wget https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.30.0/deploy/static/provider/baremetal/service-nodeport.yaml&#x000A;&#x000A;# 修改mandatory.yaml文件中的仓库&#x000A;# 修改quay.io/kubernetes-ingress-controller/nginx-ingress-controller:0.30.0&#x000A;# 为quay-mirror.qiniu.com/kubernetes-ingress-controller/nginx-ingress-controller:0.30.0&#x000A;# 创建ingress-nginx&#x000A;[root@k8s-master01 ingress-controller]# kubectl apply -f ./&#x000A;&#x000A;# 查看ingress-nginx&#x000A;[root@k8s-master01 ingress-controller]# kubectl get pod -n ingress-nginx&#x000A;NAME                                           READY   STATUS    RESTARTS   AGE&#x000A;pod/nginx-ingress-controller-fbf967dd5-4qpbp   1/1     Running   0          12h&#x000A;&#x000A;# 查看service&#x000A;[root@k8s-master01 ingress-controller]# kubectl get svc -n ingress-nginx&#x000A;NAME            TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)                      AGE&#x000A;ingress-nginx   NodePort   10.98.75.163   &lt;none&gt;        80:32240/TCP,443:31335/TCP   11h&#x000A;```&#x000A;&#x000A;##### 7.5.2 准备service和pod&#x000A;&#x000A;为了后面的实验比较方便，创建如下图所示的模型&#x000A;&#x000A;![img](Kubenetes.assets/image-20200516102419998.png)&#x000A;&#x000A;创建tomcat-nginx.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: apps/v1&#x000A;kind: Deployment&#x000A;metadata:&#x000A;  name: nginx-deployment&#x000A;  namespace: dev&#x000A;spec:&#x000A;  replicas: 3&#x000A;  selector:&#x000A;    matchLabels:&#x000A;      app: nginx-pod&#x000A;  template:&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: nginx-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: nginx&#x000A;        image: nginx:1.17.1&#x000A;        ports:&#x000A;        - containerPort: 80&#x000A;&#x000A;---&#x000A;&#x000A;apiVersion: apps/v1&#x000A;kind: Deployment&#x000A;metadata:&#x000A;  name: tomcat-deployment&#x000A;  namespace: dev&#x000A;spec:&#x000A;  replicas: 3&#x000A;  selector:&#x000A;    matchLabels:&#x000A;      app: tomcat-pod&#x000A;  template:&#x000A;    metadata:&#x000A;      labels:&#x000A;        app: tomcat-pod&#x000A;    spec:&#x000A;      containers:&#x000A;      - name: tomcat&#x000A;        image: tomcat:8.5-jre10-slim&#x000A;        ports:&#x000A;        - containerPort: 8080&#x000A;&#x000A;---&#x000A;&#x000A;apiVersion: v1&#x000A;kind: Service&#x000A;metadata:&#x000A;  name: nginx-service&#x000A;  namespace: dev&#x000A;spec:&#x000A;  selector:&#x000A;    app: nginx-pod&#x000A;  clusterIP: None&#x000A;  type: ClusterIP&#x000A;  ports:&#x000A;  - port: 80&#x000A;    targetPort: 80&#x000A;&#x000A;---&#x000A;&#x000A;apiVersion: v1&#x000A;kind: Service&#x000A;metadata:&#x000A;  name: tomcat-service&#x000A;  namespace: dev&#x000A;spec:&#x000A;  selector:&#x000A;    app: tomcat-pod&#x000A;  clusterIP: None&#x000A;  type: ClusterIP&#x000A;  ports:&#x000A;  - port: 8080&#x000A;    targetPort: 8080&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建&#x000A;[root@k8s-master01 ~]# kubectl create -f tomcat-nginx.yaml&#x000A;&#x000A;# 查看&#x000A;[root@k8s-master01 ~]# kubectl get svc -n dev&#x000A;NAME             TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)    AGE&#x000A;nginx-service    ClusterIP   None         &lt;none&gt;        80/TCP     48s&#x000A;tomcat-service   ClusterIP   None         &lt;none&gt;        8080/TCP   48s&#x000A;```&#x000A;&#x000A;##### 7.5.3 Http代理&#x000A;&#x000A;创建ingress-http.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: extensions/v1beta1&#x000A;kind: Ingress&#x000A;metadata:&#x000A;  name: ingress-http&#x000A;  namespace: dev&#x000A;spec:&#x000A;  rules:&#x000A;  - host: nginx.itheima.com&#x000A;    http:&#x000A;      paths:&#x000A;      - path: /&#x000A;        backend:&#x000A;          serviceName: nginx-service&#x000A;          servicePort: 80&#x000A;  - host: tomcat.itheima.com&#x000A;    http:&#x000A;      paths:&#x000A;      - path: /&#x000A;        backend:&#x000A;          serviceName: tomcat-service&#x000A;          servicePort: 8080&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建&#x000A;[root@k8s-master01 ~]# kubectl create -f ingress-http.yaml&#x000A;ingress.extensions/ingress-http created&#x000A;&#x000A;# 查看&#x000A;[root@k8s-master01 ~]# kubectl get ing ingress-http -n dev&#x000A;NAME           HOSTS                                  ADDRESS   PORTS   AGE&#x000A;ingress-http   nginx.itheima.com,tomcat.itheima.com             80      22s&#x000A;&#x000A;# 查看详情&#x000A;[root@k8s-master01 ~]# kubectl describe ing ingress-http  -n dev&#x000A;...&#x000A;Rules:&#x000A;Host                Path  Backends&#x000A;----                ----  --------&#x000A;nginx.itheima.com   / nginx-service:80 (10.244.1.96:80,10.244.1.97:80,10.244.2.112:80)&#x000A;tomcat.itheima.com  / tomcat-service:8080(10.244.1.94:8080,10.244.1.95:8080,10.244.2.111:8080)&#x000A;...&#x000A;&#x000A;# 接下来,在本地电脑上配置host文件,解析上面的两个域名到192.168.109.100(master)上&#x000A;# 然后,就可以分别访问tomcat.itheima.com:32240  和  nginx.itheima.com:32240 查看效果了&#x000A;```&#x000A;&#x000A;##### 7.5.4 Https代理&#x000A;&#x000A;创建证书&#x000A;&#x000A;```shell&#x000A;# 生成证书&#x000A;openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout tls.key -out tls.crt -subj &quot;/C=CN/ST=BJ/L=BJ/O=nginx/CN=itheima.com&quot;&#x000A;&#x000A;# 创建密钥&#x000A;kubectl create secret tls tls-secret --key tls.key --cert tls.crt&#x000A;```&#x000A;&#x000A;创建ingress-https.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: extensions/v1beta1&#x000A;kind: Ingress&#x000A;metadata:&#x000A;  name: ingress-https&#x000A;  namespace: dev&#x000A;spec:&#x000A;  tls:&#x000A;    - hosts:&#x000A;      - nginx.itheima.com&#x000A;      - tomcat.itheima.com&#x000A;      secretName: tls-secret # 指定秘钥&#x000A;  rules:&#x000A;  - host: nginx.itheima.com&#x000A;    http:&#x000A;      paths:&#x000A;      - path: /&#x000A;        backend:&#x000A;          serviceName: nginx-service&#x000A;          servicePort: 80&#x000A;  - host: tomcat.itheima.com&#x000A;    http:&#x000A;      paths:&#x000A;      - path: /&#x000A;        backend:&#x000A;          serviceName: tomcat-service&#x000A;          servicePort: 8080&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建&#x000A;[root@k8s-master01 ~]# kubectl create -f ingress-https.yaml&#x000A;ingress.extensions/ingress-https created&#x000A;&#x000A;# 查看&#x000A;[root@k8s-master01 ~]# kubectl get ing ingress-https -n dev&#x000A;NAME            HOSTS                                  ADDRESS         PORTS     AGE&#x000A;ingress-https   nginx.itheima.com,tomcat.itheima.com   10.104.184.38   80, 443   2m42s&#x000A;&#x000A;# 查看详情&#x000A;[root@k8s-master01 ~]# kubectl describe ing ingress-https -n dev&#x000A;...&#x000A;TLS:&#x000A;  tls-secret terminates nginx.itheima.com,tomcat.itheima.com&#x000A;Rules:&#x000A;Host              Path Backends&#x000A;----              ---- --------&#x000A;nginx.itheima.com  /  nginx-service:80 (10.244.1.97:80,10.244.1.98:80,10.244.2.119:80)&#x000A;tomcat.itheima.com /  tomcat-service:8080(10.244.1.99:8080,10.244.2.117:8080,10.244.2.120:8080)&#x000A;...&#x000A;&#x000A;# 下面可以通过浏览器访问https://nginx.itheima.com:31335 和 https://tomcat.itheima.com:31335来查看了&#x000A;```&#x000A;&#x000A;### 8. 数据存储&#x000A;&#x000A;在前面已经提到，容器的生命周期可能很短，会被频繁地创建和销毁。那么容器在销毁时，保存在容器中的数据也会被清除。这种结果对用户来说，在某些情况下是不乐意看到的。为了持久化保存容器的数据，kubernetes引入了Volume的概念。&#x000A;&#x000A;Volume是Pod中能够被多个容器访问的共享目录，它被定义在Pod上，然后被一个Pod里的多个容器挂载到具体的文件目录下，kubernetes通过Volume实现同一个Pod中不同容器之间的数据共享以及数据的持久化存储。Volume的生命容器不与Pod中单个容器的生命周期相关，当容器终止或者重启时，Volume中的数据也不会丢失。&#x000A;&#x000A;kubernetes的Volume支持多种类型，比较常见的有下面几个：&#x000A;&#x000A;- 简单存储：EmptyDir、HostPath、NFS&#x000A;- 高级存储：PV、PVC&#x000A;- 配置存储：ConfigMap、Secret&#x000A;&#x000A;#### 8.1 基本存储&#x000A;&#x000A;##### 8.1.1 EmptyDir&#x000A;&#x000A;EmptyDir是最基础的Volume类型，一个EmptyDir就是Host上的一个空目录。&#x000A;&#x000A;EmptyDir是在Pod被分配到Node时创建的，它的初始内容为空，并且无须指定宿主机上对应的目录文件，因为kubernetes会自动分配一个目录，当Pod销毁时， EmptyDir中的数据也会被永久删除。 EmptyDir用途如下：&#x000A;&#x000A;- 临时空间，例如用于某些应用程序运行时所需的临时目录，且无须永久保留&#x000A;- 一个容器需要从另一个容器中获取数据的目录（多容器共享目录）&#x000A;&#x000A;接下来，通过一个容器之间文件共享的案例来使用一下EmptyDir。&#x000A;&#x000A;在一个Pod中准备两个容器nginx和busybox，然后声明一个Volume分别挂在到两个容器的目录中，然后nginx容器负责向Volume中写日志，busybox中通过命令将日志内容读到控制台。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200413174713773.png)&#x000A;&#x000A;创建一个volume-emptydir.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: volume-emptydir&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    ports:&#x000A;    - containerPort: 80&#x000A;    volumeMounts:  # 将logs-volume挂在到nginx容器中，对应的目录为 /var/log/nginx&#x000A;    - name: logs-volume&#x000A;      mountPath: /var/log/nginx&#x000A;  - name: busybox&#x000A;    image: busybox:1.30&#x000A;    command: [&quot;/bin/sh&quot;,&quot;-c&quot;,&quot;tail -f /logs/access.log&quot;] # 初始命令，动态读取指定文件中内容&#x000A;    volumeMounts:  # 将logs-volume 挂在到busybox容器中，对应的目录为 /logs&#x000A;    - name: logs-volume&#x000A;      mountPath: /logs&#x000A;  volumes: # 声明volume， name为logs-volume，类型为emptyDir&#x000A;  - name: logs-volume&#x000A;    emptyDir: {}&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f volume-emptydir.yaml&#x000A;pod/volume-emptydir created&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pods volume-emptydir -n dev -o wide&#x000A;NAME                  READY   STATUS    RESTARTS   AGE      IP       NODE   ...... &#x000A;volume-emptydir       2/2     Running   0          97s   10.42.2.9   node1  ......&#x000A;&#x000A;# 通过podIp访问nginx&#x000A;[root@k8s-master01 ~]# curl 10.42.2.9&#x000A;......&#x000A;&#x000A;# 通过kubectl logs命令查看指定容器的标准输出&#x000A;[root@k8s-master01 ~]# kubectl logs -f volume-emptydir -n dev -c busybox&#x000A;10.42.1.0 - - [27/Jun/2021:15:08:54 +0000] &quot;GET / HTTP/1.1&quot; 200 612 &quot;-&quot; &quot;curl/7.29.0&quot; &quot;-&quot;&#x000A;```&#x000A;&#x000A;##### 8.1.2 HostPath&#x000A;&#x000A;上节课提到，EmptyDir中数据不会被持久化，它会随着Pod的结束而销毁，如果想简单的将数据持久化到主机中，可以选择HostPath。&#x000A;&#x000A;HostPath就是将Node主机中一个实际目录挂在到Pod中，以供容器使用，这样的设计就可以保证Pod销毁了，但是数据依据可以存在于Node主机上。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200413214031331.png)&#x000A;&#x000A;创建一个volume-hostpath.yaml：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: volume-hostpath&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    ports:&#x000A;    - containerPort: 80&#x000A;    volumeMounts:&#x000A;    - name: logs-volume&#x000A;      mountPath: /var/log/nginx&#x000A;  - name: busybox&#x000A;    image: busybox:1.30&#x000A;    command: [&quot;/bin/sh&quot;,&quot;-c&quot;,&quot;tail -f /logs/access.log&quot;]&#x000A;    volumeMounts:&#x000A;    - name: logs-volume&#x000A;      mountPath: /logs&#x000A;  volumes:&#x000A;  - name: logs-volume&#x000A;    hostPath: &#x000A;      path: /root/logs&#x000A;      type: DirectoryOrCreate  # 目录存在就使用，不存在就先创建后使用&#x000A;```&#x000A;&#x000A;```&#x000A;关于type的值的一点说明：&#x000A;    DirectoryOrCreate 目录存在就使用，不存在就先创建后使用&#x000A;    Directory   目录必须存在&#x000A;    FileOrCreate  文件存在就使用，不存在就先创建后使用&#x000A;    File 文件必须存在 &#x000A;    Socket  unix套接字必须存在&#x000A;    CharDevice  字符设备必须存在&#x000A;    BlockDevice 块设备必须存在&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建Pod&#x000A;[root@k8s-master01 ~]# kubectl create -f volume-hostpath.yaml&#x000A;pod/volume-hostpath created&#x000A;&#x000A;# 查看Pod&#x000A;[root@k8s-master01 ~]# kubectl get pods volume-hostpath -n dev -o wide&#x000A;NAME                  READY   STATUS    RESTARTS   AGE   IP             NODE   ......&#x000A;pod-volume-hostpath   2/2     Running   0          16s   10.42.2.10     node1  ......&#x000A;&#x000A;#访问nginx&#x000A;[root@k8s-master01 ~]# curl 10.42.2.10&#x000A;&#x000A;[root@k8s-master01 ~]# kubectl logs -f volume-emptydir -n dev -c busybox&#x000A;&#x000A;# 接下来就可以去host的/root/logs目录下查看存储的文件了&#x000A;###  注意: 下面的操作需要到Pod所在的节点运行（案例中是node1）&#x000A;[root@node1 ~]# ls /root/logs/&#x000A;access.log  error.log&#x000A;&#x000A;# 同样的道理，如果在此目录下创建一个文件，到容器中也是可以看到的&#x000A;```&#x000A;&#x000A;##### 8.1.3 NFS&#x000A;&#x000A;HostPath可以解决数据持久化的问题，但是一旦Node节点故障了，Pod如果转移到了别的节点，又会出现问题了，此时需要准备单独的网络存储系统，比较常用的用NFS、CIFS。&#x000A;&#x000A;NFS是一个网络文件存储系统，可以搭建一台NFS服务器，然后将Pod中的存储直接连接到NFS系统上，这样的话，无论Pod在节点上怎么转移，只要Node跟NFS的对接没问题，数据就可以成功访问。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200413215133559.png)&#x000A;&#x000A;1）首先要准备nfs的服务器，这里为了简单，直接是master节点做nfs服务器&#x000A;&#x000A;```shell&#x000A;# 在nfs上安装nfs服务&#x000A;[root@nfs ~]# yum install nfs-utils -y&#x000A;&#x000A;# 准备一个共享目录&#x000A;[root@nfs ~]# mkdir /root/data/nfs -pv&#x000A;&#x000A;# 将共享目录以读写权限暴露给192.168.5.0/24网段中的所有主机&#x000A;[root@nfs ~]# vim /etc/exports&#x000A;[root@nfs ~]# more /etc/exports&#x000A;/root/data/nfs     192.168.5.0/24(rw,no_root_squash)&#x000A;&#x000A;# 启动nfs服务&#x000A;[root@nfs ~]# systemctl restart nfs&#x000A;```&#x000A;&#x000A;2）接下来，要在的每个node节点上都安装下nfs，这样的目的是为了node节点可以驱动nfs设备&#x000A;&#x000A;```shell&#x000A;# 在node上安装nfs服务，注意不需要启动&#x000A;[root@k8s-master01 ~]# yum install nfs-utils -y&#x000A;```&#x000A;&#x000A;3）接下来，就可以编写pod的配置文件了，创建volume-nfs.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: volume-nfs&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    ports:&#x000A;    - containerPort: 80&#x000A;    volumeMounts:&#x000A;    - name: logs-volume&#x000A;      mountPath: /var/log/nginx&#x000A;  - name: busybox&#x000A;    image: busybox:1.30&#x000A;    command: [&quot;/bin/sh&quot;,&quot;-c&quot;,&quot;tail -f /logs/access.log&quot;] &#x000A;    volumeMounts:&#x000A;    - name: logs-volume&#x000A;      mountPath: /logs&#x000A;  volumes:&#x000A;  - name: logs-volume&#x000A;    nfs:&#x000A;      server: 192.168.5.6  #nfs服务器地址&#x000A;      path: /root/data/nfs #共享文件路径&#x000A;```&#x000A;&#x000A;4）最后，运行下pod，观察结果&#x000A;&#x000A;```shell&#x000A;# 创建pod&#x000A;[root@k8s-master01 ~]# kubectl create -f volume-nfs.yaml&#x000A;pod/volume-nfs created&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pods volume-nfs -n dev&#x000A;NAME                  READY   STATUS    RESTARTS   AGE&#x000A;volume-nfs        2/2     Running   0          2m9s&#x000A;&#x000A;# 查看nfs服务器上的共享目录，发现已经有文件了&#x000A;[root@k8s-master01 ~]# ls /root/data/&#x000A;access.log  error.log&#x000A;```&#x000A;&#x000A;#### 8.2 高级存储&#x000A;&#x000A;前面已经学习了使用NFS提供存储，此时就要求用户会搭建NFS系统，并且会在yaml配置nfs。由于kubernetes支持的存储系统有很多，要求客户全都掌握，显然不现实。为了能够屏蔽底层存储实现的细节，方便用户使用， kubernetes引入PV和PVC两种资源对象。&#x000A;&#x000A;- PV（Persistent Volume）是持久化卷的意思，是对底层的共享存储的一种抽象。一般情况下PV由kubernetes管理员进行创建和配置，它与底层具体的共享存储技术有关，并通过插件完成与共享存储的对接。&#x000A;&#x000A;- PVC（Persistent Volume Claim）是持久卷声明的意思，是用户对于存储需求的一种声明。换句话说，PVC其实就是用户向kubernetes系统发出的一种资源需求申请。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200514194111567.png)&#x000A;&#x000A;使用了PV和PVC之后，工作可以得到进一步的细分：&#x000A;&#x000A;- 存储：存储工程师维护&#x000A;- PV： kubernetes管理员维护&#x000A;- PVC：kubernetes用户维护&#x000A;&#x000A;##### 8.2.1 PV&#x000A;&#x000A;PV是存储资源的抽象，下面是资源清单文件:&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1  &#x000A;kind: PersistentVolume&#x000A;metadata:&#x000A;  name: pv2&#x000A;spec:&#x000A;  nfs: # 存储类型，与底层真正存储对应&#x000A;  capacity:  # 存储能力，目前只支持存储空间的设置&#x000A;    storage: 2Gi&#x000A;  accessModes:  # 访问模式&#x000A;  storageClassName: # 存储类别&#x000A;  persistentVolumeReclaimPolicy: # 回收策略&#x000A;```&#x000A;&#x000A;PV 的关键配置参数说明：&#x000A;&#x000A;- **存储类型**&#x000A;&#x000A;  底层实际存储的类型，kubernetes支持多种存储类型，每种存储类型的配置都有所差异&#x000A;&#x000A;- **存储能力（capacity）**&#x000A;&#x000A;目前只支持存储空间的设置( storage=1Gi )，不过未来可能会加入IOPS、吞吐量等指标的配置&#x000A;&#x000A;- **访问模式（accessModes）**&#x000A;&#x000A;  用于描述用户应用对存储资源的访问权限，访问权限包括下面几种方式：&#x000A;&#x000A;  - ReadWriteOnce（RWO）：读写权限，但是只能被单个节点挂载&#x000A;  - ReadOnlyMany（ROX）： 只读权限，可以被多个节点挂载&#x000A;  - ReadWriteMany（RWX）：读写权限，可以被多个节点挂载&#x000A;&#x000A;  `需要注意的是，底层不同的存储类型可能支持的访问模式不同`&#x000A;&#x000A;- **回收策略（persistentVolumeReclaimPolicy）**&#x000A;&#x000A;  当PV不再被使用了之后，对其的处理方式。目前支持三种策略：&#x000A;&#x000A;  - Retain （保留） 保留数据，需要管理员手工清理数据&#x000A;  - Recycle（回收） 清除 PV 中的数据，效果相当于执行 rm -rf /thevolume/*&#x000A;  - Delete （删除） 与 PV 相连的后端存储完成 volume 的删除操作，当然这常见于云服务商的存储服务&#x000A;&#x000A;  `需要注意的是，底层不同的存储类型可能支持的回收策略不同`&#x000A;&#x000A;- **存储类别**&#x000A;&#x000A;  PV可以通过storageClassName参数指定一个存储类别&#x000A;&#x000A;  - 具有特定类别的PV只能与请求了该类别的PVC进行绑定&#x000A;  - 未设定类别的PV则只能与不请求任何类别的PVC进行绑定&#x000A;&#x000A;- **状态（status）**&#x000A;&#x000A;  一个 PV 的生命周期中，可能会处于4中不同的阶段：&#x000A;&#x000A;  - Available（可用）： 表示可用状态，还未被任何 PVC 绑定&#x000A;  - Bound（已绑定）： 表示 PV 已经被 PVC 绑定&#x000A;  - Released（已释放）： 表示 PVC 被删除，但是资源还未被集群重新声明&#x000A;  - Failed（失败）： 表示该 PV 的自动回收失败&#x000A;&#x000A;**实验**&#x000A;&#x000A;使用NFS作为存储，来演示PV的使用，创建3个PV，对应NFS中的3个暴露的路径。&#x000A;&#x000A;1) 准备NFS环境&#x000A;&#x000A;```shell&#x000A;# 创建目录&#x000A;[root@nfs ~]# mkdir /root/data/{pv1,pv2,pv3} -pv&#x000A;&#x000A;# 暴露服务&#x000A;[root@nfs ~]# more /etc/exports&#x000A;/root/data/pv1     192.168.5.0/24(rw,no_root_squash)&#x000A;/root/data/pv2     192.168.5.0/24(rw,no_root_squash)&#x000A;/root/data/pv3     192.168.5.0/24(rw,no_root_squash)&#x000A;&#x000A;# 重启服务&#x000A;[root@nfs ~]#  systemctl restart nfs&#x000A;```&#x000A;&#x000A;2) 创建pv.yaml&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: PersistentVolume&#x000A;metadata:&#x000A;  name:  pv1&#x000A;spec:&#x000A;  capacity: &#x000A;    storage: 1Gi&#x000A;  accessModes:&#x000A;  - ReadWriteMany&#x000A;  persistentVolumeReclaimPolicy: Retain&#x000A;  nfs:&#x000A;    path: /root/data/pv1&#x000A;    server: 192.168.5.6&#x000A;&#x000A;---&#x000A;&#x000A;apiVersion: v1&#x000A;kind: PersistentVolume&#x000A;metadata:&#x000A;  name:  pv2&#x000A;spec:&#x000A;  capacity: &#x000A;    storage: 2Gi&#x000A;  accessModes:&#x000A;  - ReadWriteMany&#x000A;  persistentVolumeReclaimPolicy: Retain&#x000A;  nfs:&#x000A;    path: /root/data/pv2&#x000A;    server: 192.168.5.6&#x000A;    &#x000A;---&#x000A;&#x000A;apiVersion: v1&#x000A;kind: PersistentVolume&#x000A;metadata:&#x000A;  name:  pv3&#x000A;spec:&#x000A;  capacity: &#x000A;    storage: 3Gi&#x000A;  accessModes:&#x000A;  - ReadWriteMany&#x000A;  persistentVolumeReclaimPolicy: Retain&#x000A;  nfs:&#x000A;    path: /root/data/pv3&#x000A;    server: 192.168.5.6&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建 pv&#x000A;[root@k8s-master01 ~]# kubectl create -f pv.yaml&#x000A;persistentvolume/pv1 created&#x000A;persistentvolume/pv2 created&#x000A;persistentvolume/pv3 created&#x000A;&#x000A;# 查看pv&#x000A;[root@k8s-master01 ~]# kubectl get pv -o wide&#x000A;NAME   CAPACITY   ACCESS MODES  RECLAIM POLICY  STATUS      AGE   VOLUMEMODE&#x000A;pv1    1Gi        RWX            Retain        Available    10s   Filesystem&#x000A;pv2    2Gi        RWX            Retain        Available    10s   Filesystem&#x000A;pv3    3Gi        RWX            Retain        Available    9s    Filesystem&#x000A;```&#x000A;&#x000A;##### 8.2.2 PVC&#x000A;&#x000A;PVC是资源的申请，用来声明对存储空间、访问模式、存储类别需求信息。下面是资源清单文件:&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: PersistentVolumeClaim&#x000A;metadata:&#x000A;  name: pvc&#x000A;  namespace: dev&#x000A;spec:&#x000A;  accessModes: # 访问模式&#x000A;  selector: # 采用标签对PV选择&#x000A;  storageClassName: # 存储类别&#x000A;  resources: # 请求空间&#x000A;    requests:&#x000A;      storage: 5Gi&#x000A;```&#x000A;&#x000A;PVC 的关键配置参数说明：&#x000A;&#x000A;- **访问模式（accessModes）**&#x000A;&#x000A;用于描述用户应用对存储资源的访问权限&#x000A;&#x000A;- **选择条件（selector）**&#x000A;&#x000A;  通过Label Selector的设置，可使PVC对于系统中己存在的PV进行筛选&#x000A;&#x000A;- **存储类别（storageClassName）**&#x000A;&#x000A;  PVC在定义时可以设定需要的后端存储的类别，只有设置了该class的pv才能被系统选出&#x000A;&#x000A;- **资源请求（Resources ）**&#x000A;&#x000A;  描述对存储资源的请求&#x000A;&#x000A;**实验**&#x000A;&#x000A;1) 创建pvc.yaml，申请pv&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: PersistentVolumeClaim&#x000A;metadata:&#x000A;  name: pvc1&#x000A;  namespace: dev&#x000A;spec:&#x000A;  accessModes: &#x000A;  - ReadWriteMany&#x000A;  resources:&#x000A;    requests:&#x000A;      storage: 1Gi&#x000A;---&#x000A;apiVersion: v1&#x000A;kind: PersistentVolumeClaim&#x000A;metadata:&#x000A;  name: pvc2&#x000A;  namespace: dev&#x000A;spec:&#x000A;  accessModes: &#x000A;  - ReadWriteMany&#x000A;  resources:&#x000A;    requests:&#x000A;      storage: 1Gi&#x000A;---&#x000A;apiVersion: v1&#x000A;kind: PersistentVolumeClaim&#x000A;metadata:&#x000A;  name: pvc3&#x000A;  namespace: dev&#x000A;spec:&#x000A;  accessModes: &#x000A;  - ReadWriteMany&#x000A;  resources:&#x000A;    requests:&#x000A;      storage: 1Gi&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建pvc&#x000A;[root@k8s-master01 ~]# kubectl create -f pvc.yaml&#x000A;persistentvolumeclaim/pvc1 created&#x000A;persistentvolumeclaim/pvc2 created&#x000A;persistentvolumeclaim/pvc3 created&#x000A;&#x000A;# 查看pvc&#x000A;[root@k8s-master01 ~]# kubectl get pvc  -n dev -o wide&#x000A;NAME   STATUS   VOLUME   CAPACITY   ACCESS MODES   STORAGECLASS   AGE   VOLUMEMODE&#x000A;pvc1   Bound    pv1      1Gi        RWX                           15s   Filesystem&#x000A;pvc2   Bound    pv2      2Gi        RWX                           15s   Filesystem&#x000A;pvc3   Bound    pv3      3Gi        RWX                           15s   Filesystem&#x000A;&#x000A;# 查看pv&#x000A;[root@k8s-master01 ~]# kubectl get pv -o wide&#x000A;NAME  CAPACITY ACCESS MODES  RECLAIM POLICY  STATUS    CLAIM       AGE     VOLUMEMODE&#x000A;pv1    1Gi        RWx        Retain          Bound    dev/pvc1    3h37m    Filesystem&#x000A;pv2    2Gi        RWX        Retain          Bound    dev/pvc2    3h37m    Filesystem&#x000A;pv3    3Gi        RWX        Retain          Bound    dev/pvc3    3h37m    Filesystem   &#x000A;```&#x000A;&#x000A;2) 创建pods.yaml, 使用pv&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod1&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: busybox&#x000A;    image: busybox:1.30&#x000A;    command: [&quot;/bin/sh&quot;,&quot;-c&quot;,&quot;while true;do echo pod1 &gt;&gt; /root/out.txt; sleep 10; done;&quot;]&#x000A;    volumeMounts:&#x000A;    - name: volume&#x000A;      mountPath: /root/&#x000A;  volumes:&#x000A;    - name: volume&#x000A;      persistentVolumeClaim:&#x000A;        claimName: pvc1&#x000A;        readOnly: false&#x000A;---&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod2&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: busybox&#x000A;    image: busybox:1.30&#x000A;    command: [&quot;/bin/sh&quot;,&quot;-c&quot;,&quot;while true;do echo pod2 &gt;&gt; /root/out.txt; sleep 10; done;&quot;]&#x000A;    volumeMounts:&#x000A;    - name: volume&#x000A;      mountPath: /root/&#x000A;  volumes:&#x000A;    - name: volume&#x000A;      persistentVolumeClaim:&#x000A;        claimName: pvc2&#x000A;        readOnly: false&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pods.yaml&#x000A;pod/pod1 created&#x000A;pod/pod2 created&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pods -n dev -o wide&#x000A;NAME   READY   STATUS    RESTARTS   AGE   IP            NODE   &#x000A;pod1   1/1     Running   0          14s   10.244.1.69   node1   &#x000A;pod2   1/1     Running   0          14s   10.244.1.70   node1  &#x000A;&#x000A;# 查看pvc&#x000A;[root@k8s-master01 ~]# kubectl get pvc -n dev -o wide&#x000A;NAME   STATUS   VOLUME   CAPACITY   ACCESS MODES      AGE   VOLUMEMODE&#x000A;pvc1   Bound    pv1      1Gi        RWX               94m   Filesystem&#x000A;pvc2   Bound    pv2      2Gi        RWX               94m   Filesystem&#x000A;pvc3   Bound    pv3      3Gi        RWX               94m   Filesystem&#x000A;&#x000A;# 查看pv&#x000A;[root@k8s-master01 ~]# kubectl get pv -n dev -o wide&#x000A;NAME   CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM       AGE     VOLUMEMODE&#x000A;pv1    1Gi        RWX            Retain           Bound    dev/pvc1    5h11m   Filesystem&#x000A;pv2    2Gi        RWX            Retain           Bound    dev/pvc2    5h11m   Filesystem&#x000A;pv3    3Gi        RWX            Retain           Bound    dev/pvc3    5h11m   Filesystem&#x000A;&#x000A;# 查看nfs中的文件存储&#x000A;[root@nfs ~]# more /root/data/pv1/out.txt&#x000A;node1&#x000A;node1&#x000A;[root@nfs ~]# more /root/data/pv2/out.txt&#x000A;node2&#x000A;node2&#x000A;```&#x000A;&#x000A;##### 8.2.3 生命周期&#x000A;&#x000A;PVC和PV是一一对应的，PV和PVC之间的相互作用遵循以下生命周期：&#x000A;&#x000A;- **资源供应**：管理员手动创建底层存储和PV&#x000A;&#x000A;- **资源绑定**：用户创建PVC，kubernetes负责根据PVC的声明去寻找PV，并绑定&#x000A;&#x000A;  在用户定义好PVC之后，系统将根据PVC对存储资源的请求在已存在的PV中选择一个满足条件的&#x000A;&#x000A;  - 一旦找到，就将该PV与用户定义的PVC进行绑定，用户的应用就可以使用这个PVC了&#x000A;  - 如果找不到，PVC则会无限期处于Pending状态，直到等到系统管理员创建了一个符合其要求的PV&#x000A;&#x000A;  PV一旦绑定到某个PVC上，就会被这个PVC独占，不能再与其他PVC进行绑定了&#x000A;&#x000A;- **资源使用**：用户可在pod中像volume一样使用pvc&#x000A;&#x000A;  Pod使用Volume的定义，将PVC挂载到容器内的某个路径进行使用。&#x000A;&#x000A;- **资源释放**：用户删除pvc来释放pv&#x000A;&#x000A;  当存储资源使用完毕后，用户可以删除PVC，与该PVC绑定的PV将会被标记为“已释放”，但还不能立刻与其他PVC进行绑定。通过之前PVC写入的数据可能还被留在存储设备上，只有在清除之后该PV才能再次使用。&#x000A;&#x000A;- **资源回收**：kubernetes根据pv设置的回收策略进行资源的回收&#x000A;&#x000A;  对于PV，管理员可以设定回收策略，用于设置与之绑定的PVC释放资源之后如何处理遗留数据的问题。只有PV的存储空间完成回收，才能供新的PVC绑定和使用&#x000A;&#x000A;![img](Kubenetes.assets/image-20200515002806726.png)&#x000A;&#x000A;#### 8.3 配置存储&#x000A;&#x000A;##### 8.3.1 ConfigMap&#x000A;&#x000A;ConfigMap是一种比较特殊的存储卷，它的主要作用是用来存储配置信息的。&#x000A;&#x000A;创建configmap.yaml，内容如下：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: ConfigMap&#x000A;metadata:&#x000A;  name: configmap&#x000A;  namespace: dev&#x000A;data:&#x000A;  info: |&#x000A;    username:admin&#x000A;    password:123456&#x000A;```&#x000A;&#x000A;接下来，使用此配置文件创建configmap&#x000A;&#x000A;```shell&#x000A;# 创建configmap&#x000A;[root@k8s-master01 ~]# kubectl create -f configmap.yaml&#x000A;configmap/configmap created&#x000A;&#x000A;# 查看configmap详情&#x000A;[root@k8s-master01 ~]# kubectl describe cm configmap -n dev&#x000A;Name:         configmap&#x000A;Namespace:    dev&#x000A;Labels:       &lt;none&gt;&#x000A;Annotations:  &lt;none&gt;&#x000A;&#x000A;Data&#x000A;====&#x000A;info:&#x000A;----&#x000A;username:admin&#x000A;password:123456&#x000A;&#x000A;Events:  &lt;none&gt;&#x000A;```&#x000A;&#x000A;接下来创建一个pod-configmap.yaml，将上面创建的configmap挂载进去&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-configmap&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    volumeMounts: # 将configmap挂载到目录&#x000A;    - name: config&#x000A;      mountPath: /configmap/config&#x000A;  volumes: # 引用configmap&#x000A;  - name: config&#x000A;    configMap:&#x000A;      name: configmap&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-configmap.yaml&#x000A;pod/pod-configmap created&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pod pod-configmap -n dev&#x000A;NAME            READY   STATUS    RESTARTS   AGE&#x000A;pod-configmap   1/1     Running   0          6s&#x000A;&#x000A;#进入容器&#x000A;[root@k8s-master01 ~]# kubectl exec -it pod-configmap -n dev /bin/sh&#x000A;# cd /configmap/config/&#x000A;# ls&#x000A;info&#x000A;# more info&#x000A;username:admin&#x000A;password:123456&#x000A;&#x000A;# 可以看到映射已经成功，每个configmap都映射成了一个目录&#x000A;# key---&gt;文件     value----&gt;文件中的内容&#x000A;# 此时如果更新configmap的内容, 容器中的值也会动态更新&#x000A;```&#x000A;&#x000A;##### 8.3.2 Secret&#x000A;&#x000A;在kubernetes中，还存在一种和ConfigMap非常类似的对象，称为Secret对象。它主要用于存储敏感信息，例如密码、秘钥、证书等等。&#x000A;&#x000A;1) 首先使用base64对数据进行编码&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 ~]# echo -n 'admin' | base64 #准备username&#x000A;YWRtaW4=&#x000A;[root@k8s-master01 ~]# echo -n '123456' | base64 #准备password&#x000A;MTIzNDU2&#x000A;```&#x000A;&#x000A;2) 接下来编写secret.yaml，并创建Secret&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Secret&#x000A;metadata:&#x000A;  name: secret&#x000A;  namespace: dev&#x000A;type: Opaque&#x000A;data:&#x000A;  username: YWRtaW4=&#x000A;  password: MTIzNDU2&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建secret&#x000A;[root@k8s-master01 ~]# kubectl create -f secret.yaml&#x000A;secret/secret created&#x000A;&#x000A;# 查看secret详情&#x000A;[root@k8s-master01 ~]# kubectl describe secret secret -n dev&#x000A;Name:         secret&#x000A;Namespace:    dev&#x000A;Labels:       &lt;none&gt;&#x000A;Annotations:  &lt;none&gt;&#x000A;Type:  Opaque&#x000A;Data&#x000A;====&#x000A;password:  6 bytes&#x000A;username:  5 bytes&#x000A;```&#x000A;&#x000A;3) 创建pod-secret.yaml，将上面创建的secret挂载进去：&#x000A;&#x000A;```yaml&#x000A;apiVersion: v1&#x000A;kind: Pod&#x000A;metadata:&#x000A;  name: pod-secret&#x000A;  namespace: dev&#x000A;spec:&#x000A;  containers:&#x000A;  - name: nginx&#x000A;    image: nginx:1.17.1&#x000A;    volumeMounts: # 将secret挂载到目录&#x000A;    - name: config&#x000A;      mountPath: /secret/config&#x000A;  volumes:&#x000A;  - name: config&#x000A;    secret:&#x000A;      secretName: secret&#x000A;```&#x000A;&#x000A;```shell&#x000A;# 创建pod&#x000A;[root@k8s-master01 ~]# kubectl create -f pod-secret.yaml&#x000A;pod/pod-secret created&#x000A;&#x000A;# 查看pod&#x000A;[root@k8s-master01 ~]# kubectl get pod pod-secret -n dev&#x000A;NAME            READY   STATUS    RESTARTS   AGE&#x000A;pod-secret      1/1     Running   0          2m28s&#x000A;&#x000A;# 进入容器，查看secret信息，发现已经自动解码了&#x000A;[root@k8s-master01 ~]# kubectl exec -it pod-secret /bin/sh -n dev&#x000A;/ # ls /secret/config/&#x000A;password  username&#x000A;/ # more /secret/config/username&#x000A;admin&#x000A;/ # more /secret/config/password&#x000A;123456&#x000A;```&#x000A;&#x000A;至此，已经实现了利用secret实现了信息的编码。&#x000A;&#x000A;### 9. 安全认证&#x000A;&#x000A;#### 9.1 访问控制概述&#x000A;&#x000A;Kubernetes作为一个分布式集群的管理工具，保证集群的安全性是其一个重要的任务。所谓的安全性其实就是保证对Kubernetes的各种**客户端**进行**认证和鉴权**操作。&#x000A;&#x000A;**客户端**&#x000A;&#x000A;在Kubernetes集群中，客户端通常有两类：&#x000A;&#x000A;- **User Account**：一般是独立于kubernetes之外的其他服务管理的用户账号。&#x000A;- **Service Account**：kubernetes管理的账号，用于为Pod中的服务进程在访问Kubernetes时提供身份标识。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200520102949189.png)&#x000A;&#x000A;**认证、授权与准入控制**&#x000A;&#x000A;ApiServer是访问及管理资源对象的唯一入口。任何一个请求访问ApiServer，都要经过下面三个流程：&#x000A;&#x000A;- Authentication（认证）：身份鉴别，只有正确的账号才能够通过认证&#x000A;- Authorization（授权）： 判断用户是否有权限对访问的资源执行特定的动作&#x000A;- Admission Control（准入控制）：用于补充授权机制以实现更加精细的访问控制功能。&#x000A;&#x000A;![img](Kubenetes.assets/image-20200520103942580.png)&#x000A;&#x000A;#### 9.2 认证管理&#x000A;&#x000A;Kubernetes集群安全的最关键点在于如何识别并认证客户端身份，它提供了3种客户端身份认证方式：&#x000A;&#x000A;- HTTP Base认证：通过用户名+密码的方式认证&#x000A;&#x000A;  ```&#x000A;      这种认证方式是把“用户名:密码”用BASE64算法进行编码后的字符串放在HTTP请求中的Header Authorization域里发送给服务端。服务端收到后进行解码，获取用户名及密码，然后进行用户身份认证的过程。&#x000A;  ```&#x000A;&#x000A;- HTTP Token认证：通过一个Token来识别合法用户&#x000A;&#x000A;  ```&#x000A;      这种认证方式是用一个很长的难以被模仿的字符串--Token来表明客户身份的一种方式。每个Token对应一个用户名，当客户端发起API调用请求时，需要在HTTP Header里放入Token，API Server接到Token后会跟服务器中保存的token进行比对，然后进行用户身份认证的过程。&#x000A;  ```&#x000A;&#x000A;- HTTPS证书认证：基于CA根证书签名的双向数字证书认证方式&#x000A;&#x000A;  ```&#x000A;      这种认证方式是安全性最高的一种方式，但是同时也是操作起来最麻烦的一种方式。&#x000A;  ```&#x000A;&#x000A;![img](Kubenetes.assets/image-20200518211037434.png)&#x000A;&#x000A;**HTTPS认证大体分为3个过程：**&#x000A;&#x000A;1. 证书申请和下发&#x000A;&#x000A;   ```&#x000A;     HTTPS通信双方的服务器向CA机构申请证书，CA机构下发根证书、服务端证书及私钥给申请者&#x000A;   ```&#x000A;&#x000A;2. 客户端和服务端的双向认证&#x000A;&#x000A;   ```&#x000A;     1&gt; 客户端向服务器端发起请求，服务端下发自己的证书给客户端，&#x000A;        客户端接收到证书后，通过私钥解密证书，在证书中获得服务端的公钥，&#x000A;        客户端利用服务器端的公钥认证证书中的信息，如果一致，则认可这个服务器&#x000A;     2&gt; 客户端发送自己的证书给服务器端，服务端接收到证书后，通过私钥解密证书，&#x000A;        在证书中获得客户端的公钥，并用该公钥认证证书信息，确认客户端是否合法&#x000A;   ```&#x000A;&#x000A;3. 服务器端和客户端进行通信&#x000A;&#x000A;   ```&#x000A;     服务器端和客户端协商好加密方案后，客户端会产生一个随机的秘钥并加密，然后发送到服务器端。&#x000A;     服务器端接收这个秘钥后，双方接下来通信的所有内容都通过该随机秘钥加密&#x000A;   ```&#x000A;&#x000A;&gt; 注意: Kubernetes允许同时配置多种认证方式，只要其中任意一个方式认证通过即可&#x000A;&#x000A;#### 9.3 授权管理&#x000A;&#x000A;授权发生在认证成功之后，通过认证就可以知道请求用户是谁， 然后Kubernetes会根据事先定义的授权策略来决定用户是否有权限访问，这个过程就称为授权。&#x000A;&#x000A;每个发送到ApiServer的请求都带上了用户和资源的信息：比如发送请求的用户、请求的路径、请求的动作等，授权就是根据这些信息和授权策略进行比较，如果符合策略，则认为授权通过，否则会返回错误。&#x000A;&#x000A;API Server目前支持以下几种授权策略：&#x000A;&#x000A;- AlwaysDeny：表示拒绝所有请求，一般用于测试&#x000A;- AlwaysAllow：允许接收所有请求，相当于集群不需要授权流程（Kubernetes默认的策略）&#x000A;- ABAC：基于属性的访问控制，表示使用用户配置的授权规则对用户请求进行匹配和控制&#x000A;- Webhook：通过调用外部REST服务对用户进行授权&#x000A;- Node：是一种专用模式，用于对kubelet发出的请求进行访问控制&#x000A;- RBAC：基于角色的访问控制（kubeadm安装方式下的默认选项）&#x000A;&#x000A;RBAC(Role-Based Access Control) 基于角色的访问控制，主要是在描述一件事情：**给哪些对象授予了哪些权限**&#x000A;&#x000A;其中涉及到了下面几个概念：&#x000A;&#x000A;- 对象：User、Groups、ServiceAccount&#x000A;- 角色：代表着一组定义在资源上的可操作动作(权限)的集合&#x000A;- 绑定：将定义好的角色跟用户绑定在一起&#x000A;&#x000A;![img](Kubenetes.assets/image-20200519181209566.png)&#x000A;&#x000A;RBAC引入了4个顶级资源对象：&#x000A;&#x000A;- Role、ClusterRole：角色，用于指定一组权限&#x000A;- RoleBinding、ClusterRoleBinding：角色绑定，用于将角色（权限）赋予给对象&#x000A;&#x000A;**Role、ClusterRole**&#x000A;&#x000A;一个角色就是一组权限的集合，这里的权限都是许可形式的（白名单）。&#x000A;&#x000A;```yaml&#x000A;# Role只能对命名空间内的资源进行授权，需要指定nameapce&#x000A;kind: Role&#x000A;apiVersion: rbac.authorization.k8s.io/v1beta1&#x000A;metadata:&#x000A;  namespace: dev&#x000A;  name: authorization-role&#x000A;rules:&#x000A;- apiGroups: [&quot;&quot;]  # 支持的API组列表,&quot;&quot; 空字符串，表示核心API群&#x000A;  resources: [&quot;pods&quot;] # 支持的资源对象列表&#x000A;  verbs: [&quot;get&quot;, &quot;watch&quot;, &quot;list&quot;] # 允许的对资源对象的操作方法列表&#x000A;```&#x000A;&#x000A;```yaml&#x000A;# ClusterRole可以对集群范围内资源、跨namespaces的范围资源、非资源类型进行授权&#x000A;kind: ClusterRole&#x000A;apiVersion: rbac.authorization.k8s.io/v1beta1&#x000A;metadata:&#x000A; name: authorization-clusterrole&#x000A;rules:&#x000A;- apiGroups: [&quot;&quot;]&#x000A;  resources: [&quot;pods&quot;]&#x000A;  verbs: [&quot;get&quot;, &quot;watch&quot;, &quot;list&quot;]&#x000A;```&#x000A;&#x000A;需要详细说明的是，rules中的参数：&#x000A;&#x000A;- apiGroups: 支持的API组列表&#x000A;&#x000A;  ```bash&#x000A;  &quot;&quot;,&quot;apps&quot;, &quot;autoscaling&quot;, &quot;batch&quot;&#x000A;  ```&#x000A;&#x000A;- resources：支持的资源对象列表&#x000A;&#x000A;  ```bash&#x000A;  &quot;services&quot;, &quot;endpoints&quot;, &quot;pods&quot;,&quot;secrets&quot;,&quot;configmaps&quot;,&quot;crontabs&quot;,&quot;deployments&quot;,&quot;jobs&quot;,&#x000A;  &quot;nodes&quot;,&quot;rolebindings&quot;,&quot;clusterroles&quot;,&quot;daemonsets&quot;,&quot;replicasets&quot;,&quot;statefulsets&quot;,&#x000A;  &quot;horizontalpodautoscalers&quot;,&quot;replicationcontrollers&quot;,&quot;cronjobs&quot;&#x000A;  ```&#x000A;&#x000A;- verbs：对资源对象的操作方法列表&#x000A;&#x000A;  ```bash&#x000A;  &quot;get&quot;, &quot;list&quot;, &quot;watch&quot;, &quot;create&quot;, &quot;update&quot;, &quot;patch&quot;, &quot;delete&quot;, &quot;exec&quot;&#x000A;  ```&#x000A;&#x000A;**RoleBinding、ClusterRoleBinding**&#x000A;&#x000A;角色绑定用来把一个角色绑定到一个目标对象上，绑定目标可以是User、Group或者ServiceAccount。&#x000A;&#x000A;```yaml&#x000A;# RoleBinding可以将同一namespace中的subject绑定到某个Role下，则此subject即具有该Role定义的权限&#x000A;kind: RoleBinding&#x000A;apiVersion: rbac.authorization.k8s.io/v1beta1&#x000A;metadata:&#x000A;  name: authorization-role-binding&#x000A;  namespace: dev&#x000A;subjects:&#x000A;- kind: User&#x000A;  name: heima&#x000A;  apiGroup: rbac.authorization.k8s.io&#x000A;roleRef:&#x000A;  kind: Role&#x000A;  name: authorization-role&#x000A;  apiGroup: rbac.authorization.k8s.io&#x000A;```&#x000A;&#x000A;```yaml&#x000A;# ClusterRoleBinding在整个集群级别和所有namespaces将特定的subject与ClusterRole绑定，授予权限&#x000A;kind: ClusterRoleBinding&#x000A;apiVersion: rbac.authorization.k8s.io/v1beta1&#x000A;metadata:&#x000A; name: authorization-clusterrole-binding&#x000A;subjects:&#x000A;- kind: User&#x000A;  name: heima&#x000A;  apiGroup: rbac.authorization.k8s.io&#x000A;roleRef:&#x000A;  kind: ClusterRole&#x000A;  name: authorization-clusterrole&#x000A;  apiGroup: rbac.authorization.k8s.io&#x000A;```&#x000A;&#x000A;**RoleBinding引用ClusterRole进行授权**&#x000A;&#x000A;RoleBinding可以引用ClusterRole，对属于同一命名空间内ClusterRole定义的资源主体进行授权。&#x000A;&#x000A;```&#x000A;    一种很常用的做法就是，集群管理员为集群范围预定义好一组角色（ClusterRole），然后在多个命名空间中重复使用这些ClusterRole。这样可以大幅提高授权管理工作效率，也使得各个命名空间下的基础性授权规则与使用体验保持一致。&#x000A;```&#x000A;&#x000A;```yaml&#x000A;# 虽然authorization-clusterrole是一个集群角色，但是因为使用了RoleBinding&#x000A;# 所以heima只能读取dev命名空间中的资源&#x000A;kind: RoleBinding&#x000A;apiVersion: rbac.authorization.k8s.io/v1beta1&#x000A;metadata:&#x000A;  name: authorization-role-binding-ns&#x000A;  namespace: dev&#x000A;subjects:&#x000A;- kind: User&#x000A;  name: heima&#x000A;  apiGroup: rbac.authorization.k8s.io&#x000A;roleRef:&#x000A;  kind: ClusterRole&#x000A;  name: authorization-clusterrole&#x000A;  apiGroup: rbac.authorization.k8s.io&#x000A;```&#x000A;&#x000A;**实战：创建一个只能管理dev空间下Pods资源的账号**&#x000A;&#x000A;1) 创建账号&#x000A;&#x000A;```shell&#x000A;# 1) 创建证书&#x000A;[root@k8s-master01 pki]# cd /etc/kubernetes/pki/&#x000A;[root@k8s-master01 pki]# (umask 077;openssl genrsa -out devman.key 2048)&#x000A;&#x000A;# 2) 用apiserver的证书去签署&#x000A;# 2-1) 签名申请，申请的用户是devman,组是devgroup&#x000A;[root@k8s-master01 pki]# openssl req -new -key devman.key -out devman.csr -subj &quot;/CN=devman/O=devgroup&quot;     &#x000A;# 2-2) 签署证书&#x000A;[root@k8s-master01 pki]# openssl x509 -req -in devman.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out devman.crt -days 3650&#x000A;&#x000A;# 3) 设置集群、用户、上下文信息&#x000A;[root@k8s-master01 pki]# kubectl config set-cluster kubernetes --embed-certs=true --certificate-authority=/etc/kubernetes/pki/ca.crt --server=https://192.168.109.100:6443&#x000A;&#x000A;[root@k8s-master01 pki]# kubectl config set-credentials devman --embed-certs=true --client-certificate=/etc/kubernetes/pki/devman.crt --client-key=/etc/kubernetes/pki/devman.key&#x000A;&#x000A;[root@k8s-master01 pki]# kubectl config set-context devman@kubernetes --cluster=kubernetes --user=devman&#x000A;&#x000A;# 切换账户到devman&#x000A;[root@k8s-master01 pki]# kubectl config use-context devman@kubernetes&#x000A;Switched to context &quot;devman@kubernetes&quot;.&#x000A;&#x000A;# 查看dev下pod，发现没有权限&#x000A;[root@k8s-master01 pki]# kubectl get pods -n dev&#x000A;Error from server (Forbidden): pods is forbidden: User &quot;devman&quot; cannot list resource &quot;pods&quot; in API group &quot;&quot; in the namespace &quot;dev&quot;&#x000A;&#x000A;# 切换到admin账户&#x000A;[root@k8s-master01 pki]# kubectl config use-context kubernetes-admin@kubernetes&#x000A;Switched to context &quot;kubernetes-admin@kubernetes&quot;.&#x000A;```&#x000A;&#x000A;2） 创建Role和RoleBinding，为devman用户授权&#x000A;&#x000A;```yaml&#x000A;kind: Role&#x000A;apiVersion: rbac.authorization.k8s.io/v1beta1&#x000A;metadata:&#x000A;  namespace: dev&#x000A;  name: dev-role&#x000A;rules:&#x000A;- apiGroups: [&quot;&quot;]&#x000A;  resources: [&quot;pods&quot;]&#x000A;  verbs: [&quot;get&quot;, &quot;watch&quot;, &quot;list&quot;]&#x000A;  &#x000A;---&#x000A;&#x000A;kind: RoleBinding&#x000A;apiVersion: rbac.authorization.k8s.io/v1beta1&#x000A;metadata:&#x000A;  name: authorization-role-binding&#x000A;  namespace: dev&#x000A;subjects:&#x000A;- kind: User&#x000A;  name: devman&#x000A;  apiGroup: rbac.authorization.k8s.io&#x000A;roleRef:&#x000A;  kind: Role&#x000A;  name: dev-role&#x000A;  apiGroup: rbac.authorization.k8s.io&#x000A;```&#x000A;&#x000A;```shell&#x000A;[root@k8s-master01 pki]# kubectl create -f dev-role.yaml&#x000A;role.rbac.authorization.k8s.io/dev-role created&#x000A;rolebinding.rbac.authorization.k8s.io/authorization-role-binding created&#x000A;```&#x000A;&#x000A;3) 切换账户，再次验证&#x000A;&#x000A;```shell&#x000A;# 切换账户到devman&#x000A;[root@k8s-master01 pki]# kubectl config use-context devman@kubernetes&#x000A;Switched to context &quot;devman@kubernetes&quot;.&#x000A;&#x000A;# 再次查看&#x000A;[root@k8s-master01 pki]# kubectl get pods -n dev&#x000A;NAME                                 READY   STATUS             RESTARTS   AGE&#x000A;nginx-deployment-66cb59b984-8wp2k    1/1     Running            0          4d1h&#x000A;nginx-deployment-66cb59b984-dc46j    1/1     Running            0          4d1h&#x000A;nginx-deployment-66cb59b984-thfck    1/1     Running            0          4d1h&#x000A;&#x000A;# 为了不影响后面的学习,切回admin账户&#x000A;[root@k8s-master01 pki]# kubectl config use-context kubernetes-admin@kubernetes&#x000A;Switched to context &quot;kubernetes-admin@kubernetes&quot;.&#x000A;```&#x000A;&#x000A;#### 9.4 准入控制&#x000A;&#x000A;通过了前面的认证和授权之后，还需要经过准入控制处理通过之后，apiserver才会处理这个请求。&#x000A;&#x000A;准入控制是一个可配置的控制器列表，可以通过在Api-Server上通过命令行设置选择执行哪些准入控制器：&#x000A;&#x000A;```&#x000A;--admission-control=NamespaceLifecycle,LimitRanger,ServiceAccount,PersistentVolumeLabel,&#x000A;                      DefaultStorageClass,ResourceQuota,DefaultTolerationSeconds&#x000A;```&#x000A;&#x000A;只有当所有的准入控制器都检查通过之后，apiserver才执行该请求，否则返回拒绝。&#x000A;&#x000A;当前可配置的Admission Control准入控制如下：&#x000A;&#x000A;- AlwaysAdmit：允许所有请求&#x000A;- AlwaysDeny：禁止所有请求，一般用于测试&#x000A;- AlwaysPullImages：在启动容器之前总去下载镜像&#x000A;- DenyExecOnPrivileged：它会拦截所有想在Privileged Container上执行命令的请求&#x000A;- ImagePolicyWebhook：这个插件将允许后端的一个Webhook程序来完成admission controller的功能。&#x000A;- Service Account：实现ServiceAccount实现了自动化&#x000A;- SecurityContextDeny：这个插件将使用SecurityContext的Pod中的定义全部失效&#x000A;- ResourceQuota：用于资源配额管理目的，观察所有请求，确保在namespace上的配额不会超标&#x000A;- LimitRanger：用于资源限制管理，作用于namespace上，确保对Pod进行资源限制&#x000A;- InitialResources：为未设置资源请求与限制的Pod，根据其镜像的历史资源的使用情况进行设置&#x000A;- NamespaceLifecycle：如果尝试在一个不存在的namespace中创建资源对象，则该创建请求将被拒绝。当删除一个namespace时，系统将会删除该namespace中所有对象。&#x000A;- DefaultStorageClass：为了实现共享存储的动态供应，为未指定StorageClass或PV的PVC尝试匹配默认的StorageClass，尽可能减少用户在申请PVC时所需了解的后端存储细节&#x000A;- DefaultTolerationSeconds：这个插件为那些没有设置forgiveness tolerations并具有notready:NoExecute和unreachable:NoExecute两种taints的Pod设置默认的“容忍”时间，为5min&#x000A;- PodSecurityPolicy：这个插件用于在创建或修改Pod时决定是否根据Pod的security context和可用的PodSecurityPolicy对Pod的安全策略进行控制&#x000A;&#x000A;### 10. DashBoard&#x000A;&#x000A;之前在kubernetes中完成的所有操作都是通过命令行工具kubectl完成的。其实，为了提供更丰富的用户体验，kubernetes还开发了一个基于web的用户界面（Dashboard）。用户可以使用Dashboard部署容器化的应用，还可以监控应用的状态，执行故障排查以及管理kubernetes中各种资源。&#x000A;&#x000A;#### 10.1 部署Dashboard&#x000A;&#x000A;1) 下载yaml，并运行Dashboard&#x000A;&#x000A;```shell&#x000A;# 下载yaml&#x000A;[root@k8s-master01 ~]# wget  https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml&#x000A;&#x000A;# 修改kubernetes-dashboard的Service类型&#x000A;kind: Service&#x000A;apiVersion: v1&#x000A;metadata:&#x000A;  labels:&#x000A;    k8s-app: kubernetes-dashboard&#x000A;  name: kubernetes-dashboard&#x000A;  namespace: kubernetes-dashboard&#x000A;spec:&#x000A;  type: NodePort  # 新增&#x000A;  ports:&#x000A;    - port: 443&#x000A;      targetPort: 8443&#x000A;      nodePort: 30009  # 新增&#x000A;  selector:&#x000A;    k8s-app: kubernetes-dashboard&#x000A;&#x000A;# 部署&#x000A;[root@k8s-master01 ~]# kubectl create -f recommended.yaml&#x000A;&#x000A;# 查看namespace下的kubernetes-dashboard下的资源&#x000A;[root@k8s-master01 ~]# kubectl get pod,svc -n kubernetes-dashboard&#x000A;NAME                                            READY   STATUS    RESTARTS   AGE&#x000A;pod/dashboard-metrics-scraper-c79c65bb7-zwfvw   1/1     Running   0          111s&#x000A;pod/kubernetes-dashboard-56484d4c5-z95z5        1/1     Running   0          111s&#x000A;&#x000A;NAME                               TYPE       CLUSTER-IP      EXTERNAL-IP  PORT(S)         AGE&#x000A;service/dashboard-metrics-scraper  ClusterIP  10.96.89.218    &lt;none&gt;       8000/TCP        111s&#x000A;service/kubernetes-dashboard       NodePort   10.104.178.171  &lt;none&gt;       443:30009/TCP   111s&#x000A;```&#x000A;&#x000A;2）创建访问账户，获取token&#x000A;&#x000A;```shell&#x000A;# 创建账号&#x000A;[root@k8s-master01-1 ~]# kubectl create serviceaccount dashboard-admin -n kubernetes-dashboard&#x000A;&#x000A;# 授权&#x000A;[root@k8s-master01-1 ~]# kubectl create clusterrolebinding dashboard-admin-rb --clusterrole=cluster-admin --serviceaccount=kubernetes-dashboard:dashboard-admin&#x000A;&#x000A;# 获取账号token&#x000A;[root@k8s-master01 ~]#  kubectl get secrets -n kubernetes-dashboard | grep dashboard-admin&#x000A;dashboard-admin-token-xbqhh        kubernetes.io/service-account-token   3      2m35s&#x000A;&#x000A;[root@k8s-master01 ~]# kubectl describe secrets dashboard-admin-token-xbqhh -n kubernetes-dashboard&#x000A;Name:         dashboard-admin-token-xbqhh&#x000A;Namespace:    kubernetes-dashboard&#x000A;Labels:       &lt;none&gt;&#x000A;Annotations:  kubernetes.io/service-account.name: dashboard-admin&#x000A;              kubernetes.io/service-account.uid: 95d84d80-be7a-4d10-a2e0-68f90222d039&#x000A;&#x000A;Type:  kubernetes.io/service-account-token&#x000A;&#x000A;Data&#x000A;====&#x000A;namespace:  20 bytes&#x000A;token:      eyJhbGciOiJSUzI1NiIsImtpZCI6ImJrYkF4bW5XcDhWcmNGUGJtek5NODFuSXl1aWptMmU2M3o4LTY5a2FKS2cifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlcm5ldGVzLWRhc2hib2FyZCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJkYXNoYm9hcmQtYWRtaW4tdG9rZW4teGJxaGgiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC5uYW1lIjoiZGFzaGJvYXJkLWFkbWluIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQudWlkIjoiOTVkODRkODAtYmU3YS00ZDEwLWEyZTAtNjhmOTAyMjJkMDM5Iiwic3ViIjoic3lzdGVtOnNlcnZpY2VhY2NvdW50Omt1YmVybmV0ZXMtZGFzaGJvYXJkOmRhc2hib2FyZC1hZG1pbiJ9.NAl7e8ZfWWdDoPxkqzJzTB46sK9E8iuJYnUI9vnBaY3Jts7T1g1msjsBnbxzQSYgAG--cV0WYxjndzJY_UWCwaGPrQrt_GunxmOK9AUnzURqm55GR2RXIZtjsWVP2EBatsDgHRmuUbQvTFOvdJB4x3nXcYLN2opAaMqg3rnU2rr-A8zCrIuX_eca12wIp_QiuP3SF-tzpdLpsyRfegTJZl6YnSGyaVkC9id-cxZRb307qdCfXPfCHR_2rt5FVfxARgg_C0e3eFHaaYQO7CitxsnIoIXpOFNAR8aUrmopJyODQIPqBWUehb7FhlU1DCduHnIIXVC_UICZ-MKYewBDLw&#x000A;ca.crt:     1025 bytes&#x000A;```&#x000A;&#x000A;3）通过浏览器访问Dashboard的UI&#x000A;&#x000A;在登录页面上输入上面的token&#x000A;&#x000A;![image-20200520144548997](Kubenetes.assets/image-20200520144548997.png)&#x000A;&#x000A;出现下面的页面代表成功&#x000A;&#x000A;![image-20200520144959353](Kubenetes.assets/image-20200520144959353.png)&#x000A;&#x000A;#### 10.2 使用DashBoard&#x000A;&#x000A;本章节以Deployment为例演示DashBoard的使用&#x000A;&#x000A;**查看**&#x000A;&#x000A;选择指定的命名空间`dev`，然后点击`Deployments`，查看dev空间下的所有deployment&#x000A;&#x000A;![img](Kubenetes.assets/image-20200520154628679.png)&#x000A;&#x000A;**扩缩容**&#x000A;&#x000A;在`Deployment`上点击`规模`，然后指定`目标副本数量`，点击确定&#x000A;&#x000A;![img](Kubenetes.assets/image-20200520162605102.png)&#x000A;&#x000A;**编辑**&#x000A;&#x000A;在`Deployment`上点击`编辑`，然后修改`yaml文件`，点击确定&#x000A;&#x000A;![image-20200520163253644](Kubenetes.assets/image-20200520163253644.png)&#x000A;&#x000A;**查看Pod**&#x000A;&#x000A;点击`Pods`, 查看pods列表&#x000A;&#x000A;![img](Kubenetes.assets/image-20200520163552110.png)&#x000A;&#x000A;**操作Pod**&#x000A;&#x000A;选中某个Pod，可以对其执行日志（logs）、进入执行（exec）、编辑、删除操作&#x000A;&#x000A;&#x000A;&#x000A;&gt; Dashboard提供了kubectl的绝大部分功能，这里不再一一演示</textarea>&#x000A;<div class='loader-wrapper'>&#x000A;<div class='ui inline mini active loader'></div>&#x000A;</div></blob-markdown-renderer>&#x000A;</div>
<div class='file_line'></div>

</div>
<div class='tree_progress'>
<div class='ui active inverted dimmer'>
<div class='ui small text loader'>Loading...</div>
</div>
</div>
</div>
<div class='ui small modal' id='modal-linejump'>
<div class='ui custom form content'>
<div class='field'>
<div class='ui right action input'>
<input placeholder='Jump to line...' type='number'>
<div class='ui orange button'>
Go
</div>
</div>
</div>
</div>
</div>

<div class='complaint'>
<div class='ui modal small form' id='landing-comments-complaint-modal'>
<i class='iconfont icon-close close'></i>
<div class='header'>
Report
</div>
<div class='content'>
<div class='appeal-success-tip hide'>
<i class='iconfont icon-ic_msg_success'></i>
<div class='appeal-success-text'>
Report success
</div>
<span>
We will send you the feedback within 2 working days through the letter!
</span>
</div>
<div class='appeal-tip'>
Please fill in the reason for the report carefully. Provide as detailed a description as possible.
</div>
<div class='ui form appeal-form'>
<div class='inline field'>
<label class='left-part appeal-type-wrap'>
Type
</label>
<div class='ui dropdown selection' id='appeal-comments-types'>
<div class='text default'>
Please select a report type
</div>
<i class='dropdown icon'></i>
<div class='menu'></div>
</div>
</div>
<div class='inline field'>
<label class='left-part'>
Reason
</label>
<textarea class='appeal-reason' id='appeal-comment-reason' name='msg' placeholder='Please explain the reason for the report' rows='3'></textarea>
</div>
<div class='ui message callback-msg hide'></div>
<div class='ui small error text message exceeded-size-tip'></div>
</div>
</div>
<div class='actions'>
<div class='ui button blank cancel'>
Cancel
</div>
<div class='ui orange icon button disabled ok' id='complaint-comment-confirm'>
Send
</div>
</div>
</div>
<script>
  var $complaintCommentsModal = $('#landing-comments-complaint-modal'),
      $complainCommentType = $complaintCommentsModal.find('#appeal-comments-types'),
      $complaintModalTip = $complaintCommentsModal.find('.callback-msg'),
      $complaintCommentsContent = $complaintCommentsModal.find('.appeal-reason'),
      $complaintCommentBtn = $complaintCommentsModal.find('#complaint-comment-confirm'),
      complaintSending = false,
      initedCommentsType = false;
  
  function initCommentsTypeList() {
    if (!initedCommentsType) {
      $.ajax({
        url: "/appeals/fetch_types",
        method: 'get',
        data: {'type': 'comment'},
        success: function (data) {
          var result = '';
          for (var i = 0; i < data.length; i++) {
            result = result + "<div class='item' data-value='" + data[i].id + "'>" + data[i].name + "</div>";
          }
          $complainCommentType.find('.menu').html(result);
        }
      });
      $complainCommentType.dropdown({showOnFocus: false});
      initedCommentsType = true;
    }
  }
  $complainCommentType.on('click', function() {
    $complaintCommentsModal.modal({
      autofocus: false,
      onApprove: function() {
        return false;
      },
      onHidden: function() {
        restoreCommonentDefault();
      }
    }).modal('show');
  });
  
  $complaintCommentsContent.on('change keyup', function(e) {
    var content = $(this).val();
    if ($.trim(content).length > 0 && $complainCommentType.dropdown('get value').length > 0 ) {
      $complaintCommentBtn.removeClass('disabled');
      return;
    }
    $complaintCommentBtn.addClass('disabled');
  });
  
  
  $complainCommentType.dropdown({
    showOnFocus: false,
    onChange: function(value, text, $selectedItem) {
      if (value.length > 0 && $.trim($complaintCommentsContent.val()).length > 0) {
        $complaintCommentBtn.removeClass('disabled');
        return
      }
      $complaintCommentBtn.addClass('disabled');
    }
  });
  
  function restoreCommonentDefault() {
    $complainCommentType.dropdown('restore defaults');
    $complaintCommentsContent.val('');
    $('.exceeded-size-tip').text('').hide();
    $complaintModalTip.text('').hide();
    setTimeout(function() {
      setCommentSendTip(false);
    }, 1500);
  }
  
  $complaintCommentBtn.on('click',function(e){
    var reason = $complaintCommentsContent.val();
    var appealableId = $('#landing-comments-complaint-modal').attr('data-id');
    if (complaintSending) {
      return;
    }
    var appealType = $complainCommentType.dropdown('get value');
    var formData = new FormData();
    formData.append('appeal_type_id', appealType);
    formData.append('reason', reason);
    formData.append('appeal_type','Note');
    formData.append('target_id',appealableId);
    $.ajax({
      type: 'POST',
      url: "/appeals",
      cache: false,
      contentType: false,
      processData: false,
      data: formData,
      beforeSend: function() {
        setCommentSendStatus(true);
      },
      success: function(res) {
        if (res.status == 200) {
          setCommentSendTip(true);
          setTimeout(function() {
            $complaintCommentsModal.modal('hide');
            restoreCommonentDefault();
          }, 3000);
        }
        setCommentSendStatus(false);
      },
      error: function(err) {
        showCommonTips(err.responseJSON.message, 'error');
        setCommentSendStatus(false);
      }
    })
  });
  
  function showCommonTips(text, type) {
    $complaintModalTip.text(text).show();
    if (type == 'error') {
      $complaintModalTip.removeClass('success').addClass('error');
    } else {
      $complaintModalTip.removeClass('error').addClass('success');
    }
  }
  
  function setCommentSendStatus(value) {
    complaintSending = value;
    if (complaintSending) {
      $complaintCommentBtn.addClass('loading');
      $complaintCommentsContent.attr('readonly', true);
      $complainCommentType.attr('readonly', true);
    } else {
      $complaintCommentBtn.removeClass('loading');
      $complaintCommentsContent.attr('readonly', false);
      $complainCommentType.attr('readonly', false);
    }
  }
  
  function setCommentSendTip(value) {
    if (value) {
      $('.appeal-success-tip').removeClass('hide');
      $('.appeal-tip').addClass('hide');
      $('.appeal-form').addClass('hide');
      $('#landing-comments-complaint-modal .actions').addClass('hide');
    } else {
      $('.appeal-success-tip').addClass('hide');
      $('.appeal-tip').removeClass('hide');
      $('.appeal-form').removeClass('hide');
      $('#landing-comments-complaint-modal .actions').removeClass('hide');
    }
  }
</script>

<div class='ui small modal' id='misjudgment_appeal_modal'>
<i class='close icon'></i>
<div class='header dividing ui'>
误判申诉
</div>
<div class='content'>
<p>此处可能存在不合适展示的内容，页面不予展示。您可通过相关编辑功能自查并修改。</p>
<p>如您确认内容无涉及 不当用语 / 纯广告导流 / 暴力 / 低俗色情 / 侵权 / 盗版 / 虚假 / 无价值内容或违法国家有关法律法规的内容，可点击提交进行申诉，我们将尽快为您处理。</p>
<div class='buttons'>
<div class='ui button blank cancel'>取消</div>
<div class='ui button orange submit'>提交</div>
</div>
</div>
</div>
<style>
  #misjudgment_appeal_modal .buttons {
    float: right;
    margin-top: 30px;
    margin-bottom: 20px; }
    #misjudgment_appeal_modal .buttons .cancel {
      margin-right: 20px; }
</style>
<script>
  var $misjudgmentAppealModal = $('#misjudgment_appeal_modal');
  $('.cancel').on('click',function(){
    $misjudgmentAppealModal.modal('hide');
  });
  var $jsSubmitAppeal = $misjudgmentAppealModal.find('.submit')
  $jsSubmitAppeal.on('click', function(e) {
    e.preventDefault();
    $(this).addClass('loading').addClass('disabled');
    var type = $(this).attr('data-type');
    var id = $(this).attr('data-id');
    var projectId = $(this).attr('data-project-id');
    var appealType = $(this).attr('data-appeal-type');
    $.ajax({
      type: "PUT",
      url: "/misjudgment_appeal",
      data: {
        type: type,
        id: id,
        project_id: projectId,
        appeal_type: appealType
      },
      success: function(data) {
        Flash.info('提交成功');
        $jsSubmitAppeal.removeClass('loading');
        $misjudgmentAppealModal.modal('hide');
        location.reload()
      },
      error: function(e) {
        Flash.error('提交失败:'+e.responseText);
        $jsSubmitAppeal.removeClass('loading').removeClass('disabled');
        location.reload()
      }
    });
  })
</script>

</div>
<script>
  "use strict";
  $('.js-check-star').checkbox('set unchecked')
</script>

</div>
</div>
</div>
<div class='four wide column' style='display: none;'>
<div class='project__right-side'>
<div class='side-item intro'>
<div class='header'>
<h4>About</h4>
</div>
<div class='content'>
<span class='git-project-desc-text'>各位小伙伴，k8s 中的违规内容已经做了修复，你们可以正常使用了。gitee 这个老六，给你提示违规信息，却不给你提供那些词违规了，真的服了这个老六了，现在已经处理完了。gitee是有自己的敏感词汇检测机制，感觉很不智能。大家在写技术博客的时候注意用词，避免不必要的麻烦。大家有什么问题可以+v: yooobee 来讨论。</span>
<a class='hide spread' href='javascript:void(0);'>
expand
<i class='caret down icon'></i>
</a>
<a class='retract hide' href='javascript:void(0);'>
collapse
<i class='caret up icon'></i>
</a>
<div class='intro-list'>
<div class='blank d-flex d-flex-between dropdown item js-project-label_show label-list-line-feed project-label-list ui' data-labels='[]' data-url='/yooome/golang/update_description'>
<div class='mixed-label'>
</div>

<div class='default'>No labels</div>
</div>
<div class='hide item'>
<i class='iconfont icon-link'></i>
<span class='git-project-homepage'>
<a rel="nofollow" id="homepage" target="_blank" href=""></a>
</span>
</div>
<div class='item box-licence'>
<i class='iconfont icon-licence'></i>
<span id='license-popup'>
MulanPSL-2.0
</span>
<div class='ui popup dark'>Use MulanPSL-2.0</div>
</div>
<!-- - page = @project.page -->
<!-- - if page&.status? -->
<!-- .item -->
<!-- %i.iconfont.icon-giteepage -->
<!-- Pages： -->
<!-- = link_to page.domain_url, page.domain_url, target: '_blank' -->
<div class='item star-item'>
<i class='iconfont icon-star'></i>
<a class="action-social-count " title="1641" href="/yooome/golang/stargazers"><span class='text-bold'>
1.6K
</span>
Stars
</a></div>
<div class='item watch-item'>
<i class='iconfont icon-watch'></i>
<a class="action-social-count" title="133" href="/yooome/golang/watchers"><span class='text-bold'>
133
</span>
Watching
</a></div>
<div class='item'>
<i class='iconfont icon-fork'></i>
<a class="action-social-count disabled-style" title="1909" href="/yooome/golang/members"><span class='text-bold'>
1.9K
</span>
Forks
</a></div>
</div>
</div>
<div class='content intro-form'>
<div class='ui small input'>
<textarea name='project[description]' placeholder='Description' rows='5'></textarea>
</div>
<div class='ui small input'>
<input data-regex-value='(^$)|(^(http|https):\/\/(([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])\.){3}([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5]).*)|(^(http|https):\/\/[a-zA-Z0-9]+([_\-\.]{1}[a-zA-Z0-9]+)*\.[a-zA-Z]{2,10}(:[0-9]{1,10})?(\?.*)?(\/.*)?$)' name='project[homepage]' placeholder='Homepage(eg: https://gitee.com)' type='text'>
</div>
<button class='ui orange button mt-1 btn-save'>
Save
</button>
<div class='ui blank button btn-cancel-edit'>
Cancel
</div>
</div>
</div>
<div class='side-item release'>
<div class='header'>
<h4>Releases</h4>
</div>
<div class='content'>
<span class='text-muted'>
No release
</span>
</div>
</div>
<div class='side-item contrib' data-url='/yooome/golang/contributors_count?ref=main' id='contributor'>
<div class='header'>
<h4>
Contributors
<span class='text-muted' id='contributor-count'></span>
</h4>
<a class="ui link button pull-right" href="/yooome/golang/contributors?ref=main">All</a>
</div>
<div class='content' id='contributor-list'></div>
<div class='ui active centered inline loader' id='contributor-loader'></div>
</div>
<div class='side-item' id='languages'>
<div class='header'>
<h4>
Language(Optional)
</h4>
</div>
<div class='content'>
<div class='lang-bar-container mb-2'>
<div class='lang-bar'>
<div class='bar' style='width: 49.1%;background:#41b883'></div>
<div class='bar' style='width: 30.4%;background:#00ADD8'></div>
<div class='bar' style='width: 14.6%;background:#f1e05a'></div>
<div class='bar' style='width: 3.4%;background:#563d7c'></div>
<div class='bar' style='width: 2.4%;background:#e34c26'></div>
<div class='bar' style='width: 0.1%;background:#EDEDED'></div>
</div>
</div>
<div class='lang-legend'>
<span class='d-align-center'>
<span class='lang-dot' style='background:#41b883'></span>
<a class="lang-text" href="/explore/all?lang=Vue">Vue</a>
<a class="percentage ml-1 text-muted" href="/explore/all?lang=Vue">49.1%</a>
</span>
<span class='d-align-center'>
<span class='lang-dot' style='background:#00ADD8'></span>
<a class="lang-text" href="/explore/all?lang=Go">Go</a>
<a class="percentage ml-1 text-muted" href="/explore/all?lang=Go">30.4%</a>
</span>
<span class='d-align-center'>
<span class='lang-dot' style='background:#f1e05a'></span>
<a class="lang-text" href="/explore/all?lang=JavaScript">JavaScript</a>
<a class="percentage ml-1 text-muted" href="/explore/all?lang=JavaScript">14.6%</a>
</span>
<span class='d-align-center'>
<span class='lang-dot' style='background:#563d7c'></span>
<a class="lang-text" href="/explore/all?lang=CSS">CSS</a>
<a class="percentage ml-1 text-muted" href="/explore/all?lang=CSS">3.4%</a>
</span>
<span class='d-align-center'>
<span class='lang-dot' style='background:#e34c26'></span>
<a class="lang-text" href="/explore/all?lang=HTML">HTML</a>
<a class="percentage ml-1 text-muted" href="/explore/all?lang=HTML">2.4%</a>
</span>
<span class='d-align-center'>
<span class='lang-dot' style='background:#EDEDED'></span>
<a class="lang-text" href="/explore/all?lang=Other">Other</a>
<a class="percentage ml-1 text-muted" href="/explore/all?lang=Other">0.1%</a>
</span>
</div>
</div>
</div>

<div class='side-item events' data-url='/yooome/golang/events.json' id='proj-events'>
<div class='header'>
<h4>Activities</h4>
</div>
<div class='content'>
<div class='ui comments' id='event-list'></div>
<a class="loadmore hide" href="javascript:void(0);">Load More
<i class='icon dropdown'></i>
</a><center>
<div class='text-muted nomore hide'>can not load any more</div>
<div class='ui inline loader active'></div>
</center>
</div>
</div>
</div>
<div class='ui modal tiny' id='edit-project-description'>
<i class='iconfont icon-close close'></i>
<div class='header'>Edit</div>
<div class='content'>
<div class='item mb-2'>
<div class='title label'>About</div>
<div class='ui small input'>
<textarea maxlength='200' name='project[description]' placeholder='Description' rows='5'>各位小伙伴，k8s 中的违规内容已经做了修复，你们可以正常使用了。gitee 这个老六，给你提示违规信息，却不给你提供那些词违规了，真的服了这个老六了，现在已经处理完了。gitee是有自己的敏感词汇检测机制，感觉很不智能。大家在写技术博客的时候注意用词，避免不必要的麻烦。大家有什么问题可以+v: yooobee 来讨论。</textarea>
</div>
</div>
<div class='item mb-2'>
<div class='title label'>Homepage</div>
<div class='ui small input'>
<input data-regex-value='(^$)|(^(http|https):\/\/(([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5])\.){3}([0-9]|[1-9][0-9]|1[0-9]{2}|2[0-4][0-9]|25[0-5]).*)|(^(http|https):\/\/[a-zA-Z0-9]+([_\-\.]{1}[a-zA-Z0-9]+)*\.[a-zA-Z]{2,10}(:[0-9]{1,10})?(\?.*)?(\/.*)?$)' name='project[homepage]' placeholder='Homepage(eg: https://gitee.com)' type='text' value=''>
</div>
</div>
</div>
<div class='actions'>
<button class='ui button blank cancel'>Cancel</button>
<button class='ui button orange btn-save'>Save</button>
</div>
</div>

<style>
  #readme-name,
  #license-popup {
    color: #005980;
    cursor: pointer; }
</style>
<script>
  window.gon.projectRightSide = {
    homepage: "",
    description: "各位小伙伴，k8s 中的违规内容已经做了修复，你们可以正常使用了。gitee 这个老六，给你提示违规信息，却不给你提供那些词违规了，真的服了这个老六了，现在已经处理完了。gitee是有自己的敏感词汇检测机制，感觉很不智能。大家在写技术博客的时候注意用词，避免不必要的麻烦。大家有什么问题可以+v: yooobee 来讨论。",
    url: '/yooome/golang/update_description',
    i18n: {
      invalidHomepage: 'Invalid homepage',
      descriptionLimitExceeded: 'The length of the about shall not exceed %{limit} characters',
      noDescription: 'no description',
      noPermission: 'no permission',
      requestError: 'update error!'
    }
  }
  window.gon.cloneArrSelectedLabel = [] || []
  $(function () {
    var $editModal = $('#edit-project-description')
    $editModal.modal({
      onShow: function () {
        window.globalUtils.getFocus($editModal.find('textarea'))
      }
    })
    $('.project__right-side').on('click', '.header .btn-edit', function () {
      $editModal.modal('show')
    })
    $('#license-popup').popup({ position: 'bottom center', lastResort: 'bottom center' })
  
    $('.js-project-label_show').projectLabel({
      i18n: {
        empty: "The name cannot be empty",
        verify: "10. The name is only allowed to contain Chinese, letters, numbers or a dash (-), cannot start with a dash, and the length is less than 35 characters",
        max: "Select up to 5"
      }
    })
  })
</script>

</div>
<div class='project-right-side-contaner' id='code-parsing'>
<div class='d-flex-between mb-2'>
<div class='title fs-16 d-align-center'>
<img class='mr-1' height='32' src='/static/images/mjc_icon@2x.png' width='32'>
<span class='ai-file-name'>马建仓 AI 助手</span>
</div>
<div>
<i class='iconfont icon-close close gitee-icon-close'></i>
</div>
</div>
<div class='code-parsing-content'>
<div class='sub_title'></div>
<div class='markdown-body'></div>
<div class='bottom-content'>
<div class='js-code-parsing-img'></div>
<div class='ai_code_btns_simple'>
<div class='ai_code_btns_simple_container'>
<div class='mr-1 test-more'>尝试更多</div>
<div class='btn_box' data-content='帮我解读代码' data-text='代码解读' data-value='code_explain'>
<div class='btn_box_title'>代码解读</div>
</div>
<div class='btn_box' data-content='帮我代码找茬' data-text='代码找茬' data-value='code_review'>
<div class='btn_box_title'>代码找茬</div>
</div>
<div class='btn_box' data-content='帮我优化代码' data-text='代码优化' data-value='code_improve'>
<div class='btn_box_title'>代码优化</div>
</div>
</div>
</div>
</div>
</div>
<div class='skeleton'>
<div class='line line1'></div>
<div class='line line2'></div>
<div class='line line3'></div>
<div class='line line4'></div>
<div class='line line1'></div>
<div class='line line2'></div>
<div class='line line3'></div>
<div class='line line4'></div>
<div class='line line1'></div>
<div class='line line2'></div>
<div class='line line3'></div>
<div class='line line4'></div>
</div>
<div class='resize-handle'>
<div class='resize-handle-line'></div>
</div>
<script src="/static/javascripts/markdown-it.min.js"></script>
<script src="https://cn-assets.gitee.com/assets/ai_code_parsing/app-543d4fe951fa0e922e8c39b2442ab9a9.js"></script>
<script>
  $(function() {
    var maxWidthPercentage = 0.5;
    $("#code-parsing").resizable({
      handles: 'e, w', // 通过左边调整大小
      minWidth: 350, // 设置 代码解析框 的最小宽度
      resize: function(event, ui) {
        var parentWidth = $(this).parent().width();
        var newWidthDiv2 = ui.size.width;
        var newWidthDiv1 = parentWidth - newWidthDiv2;
        // 计算最大宽度
        var maxWidthDiv2 = parentWidth * maxWidthPercentage;
        // 确保 代码解析框 不超过最大宽度
        newWidthDiv2 = Math.min(newWidthDiv2, maxWidthDiv2);
        // 确保 文件详情 至少有最小宽度
        newWidthDiv1 = Math.max(parentWidth - newWidthDiv2, 750);
  
        var percentageCode = (newWidthDiv2 / parentWidth) * 100;
        var percentageProject = (newWidthDiv1 / parentWidth) * 100;
  
        $('#code-parsing').css('width',percentageCode+"%")
        $('.git-project-content-wrapper').find('#sixteen').attr('style', 'width: ' + percentageProject + '% !important;');
        $('.right-wrapper').attr('style', 'width: ' + percentageProject + '% !important;');
        $('.project-conter-container').attr('style', 'width: ' + percentageProject + '% !important;');
      }
    });
  })
</script>

</div>
</div>
</div>
<script>
  (function() {
    $(function() {
      Tree.init();
      return TreeCommentActions.init();
    });
  
  }).call(this);
</script>
<script>
  function scrollToReadmeBox() {
    var readmeBox = document.getElementById('git-readme');
    if (readmeBox) {
      const topPos = readmeBox.offsetTop;
      window.scrollTo({ top: topPos, behavior: "smooth" });
    }
  }
  
  $(".box-licence").click(function(event) {
    $('.lisence-content').show()
    $('.lisence-edit').show()
    $('.readme-content').hide()
    $('.readme-edit').hide()
    $('.file_title_license').addClass('active-title')
    $('.file_title_readme').removeClass('active-title')
    scrollToReadmeBox()
  });
  
  $(".box-readme").click(function(event) {
    $('.lisence-content').hide()
    $('.lisence-edit').hide()
    $('.readme-content').show()
    $('.readme-edit').show()
    $('.file_title_license').removeClass('active-title')
    $('.file_title_readme').addClass('active-title')
    scrollToReadmeBox()
  });
  
  // 防止二次挂载
  if (true) {
    window.gon.tree_left_side_loaded = true;
  }
</script>
<link rel="stylesheet" media="all" href="https://cn-assets.gitee.com/assets/markdown_preview-001478f1b12f2725f1b1f76f36b9ce4e.css" />
<script src="https://cn-assets.gitee.com/assets/markdown_preview-772822b3442a45aaf94af83c38fdbaf4.js"></script>
<script src="https://cn-assets.gitee.com/webpacks/markdown_render-b6acccaca04b17e49fdb.bundle.js" defer="defer"></script>

</div>
<script>
  (function() {
    var donateModal;
  
    Gitee.modalHelper = new GiteeModalHelper({
      alertText: '提示',
      okText: '确定'
    });
  
    donateModal = new ProjectDonateModal({
      el: '#project-donate-modal',
      alipayUrl: '/yooome/golang/alipay',
      wepayUrl: '/yooome/golang/wepay',
      nameIsBlank: 'name cannot be blank',
      nameTooLong: 'name is too long (maximum is 36 character)',
      modalHelper: Gitee.modalHelper
    });
  
    if (null === 'true') {
      donateModal.show();
    }
  
    $('#project-donate').on('click', function() {
      return donateModal.show();
    });
  
  }).call(this);
</script>
<script>
  Tree.initHighlightTheme('white')
</script>


</div>
<div class='gitee-project-extension'>
<div class='extension lang'>Go</div>
<div class='extension public'>1</div>
<div class='extension https'>https://gitee.com/yooome/golang.git</div>
<div class='extension ssh'>git@gitee.com:yooome/golang.git</div>
<div class='extension namespace'>yooome</div>
<div class='extension repo'>golang</div>
<div class='extension name'>LearningNotes</div>
<div class='extension branch'>main</div>
</div>

<script>
  $(function() {
    GitLab.GfmAutoComplete.dataSource = "/yooome/golang/autocomplete_sources"
    GitLab.GfmAutoComplete.Emoji.assetBase = '/assets/emoji'
    GitLab.GfmAutoComplete.setup();
  });
</script>

<footer id='git-footer-main'>
<div class='ui container'>
<div class='logo-row'>
<a href="https://gitee.com"><img alt='Gitee — A Git-based Code Hosting and Research Collaboration Platform' class='logo-img' src='/static/images/logo-black.svg?t=158106666'>
</a></div>
<div class='name-important'>
©OSCHINA. All rights reserved
</div>
<div class='ui two column grid d-flex-centeris-en'>
<div class='eight wide column git-footer-left'>
<div class='ui four column grid' id='footer-left'>
<div class='column'>
<div class='ui link list'>
<div class='item'>
<a class="item" href="/all-about-git">Git Resources</a>
</div>
<div class='item'>
<a class="item" rel="nofollow" href="https://help.gitee.com/learn-Git-Branching/">Learning Git</a>
</div>
<div class='item'>
<a class="item" rel="nofollow" href="https://copycat.gitee.com/">CopyCat</a>
</div>
<div class='item'>
<a class="item" href="/appclient">Downloads</a>
</div>
</div>
</div>
<div class='column'>
<div class='ui link list'>
<div class='item'>
<a class="item" href="/gitee-stars">Gitee Stars</a>
</div>
<div class='item'>
<a class="item" href="/gvp">Featured Projects</a>
</div>
<div class='item'>
<a class="item" rel="nofollow" href="https://blog.gitee.com/">Blog</a>
</div>
<div class='item'>
<a class="item" href="/enterprises#nonprofit-plan">Nonprofit</a>
</div>
<div class='item'>
<a class="item" href="https://gitee.com/features/gitee-go">Gitee Go</a>
</div>
</div>
</div>
<div class='column'>
<div class='ui link list'>
<div class='item'>
<a class="item" href="/api/v5/swagger">OpenAPI</a>
</div>
<div class='item'>
<a class="item" href="https://gitee.com/oschina/mcp-gitee">MCP Server</a>
</div>
<div class='item'>
<a class="item" href="https://help.gitee.com">Help Center</a>
</div>
<div class='item'>
<a class="item" href="/self_services">Self-services</a>
</div>
<div class='item'>
<a class="item" href="/help/articles/4378">Updates</a>
</div>
</div>
</div>
<div class='column'>
<div class='ui link list'>
<div class='item'>
<a class="item" href="/about_us">About Us</a>
</div>
<div class='item'>
<a class="item" rel="nofollow" href="https://www.oschina.net/news/131099/oschina-hiring">Join us</a>
</div>
<div class='item'>
<a class="item" href="/terms">Terms of use</a>
</div>
<div class='item'>
<a class="item" href="/oschina/git-osc/issues">Feedback</a>
</div>
<div class='item'>
<a class="item" href="/links.html">Partners</a>
</div>
</div>
</div>
</div>
</div>
<div class='eight wide column right aligned followus git-footer-right'>
<div class='qrcode mr-1'>
<div class='qrcode-box'>
<img alt="Exchange" src="https://cn-assets.gitee.com/assets/contact_qr-5e2c2a8da453396590e56a545bce4974.jpg" />
</div>
<p class='mt-1 mini_app-text'>Exchange</p>
</div>
<div class='qrcode'>
<div class='qrcode-box'>
<img alt="微信服务号" class="weixin-qr" src="https://cn-assets.gitee.com/assets/qrcode-weixin@2x-b74cc97a2ea80123ea53a737f709836d.png" />
</div>
<p class='mt-1 weixin-text'>WeChat</p>
</div>
<div class='phone-and-qq column'>
<div class='ui list official-support-container'>
<div class='item'></div>
<div class='item mail-and-zhihu'>
<a class="icon-popup" title="E-mail" rel="nofollow" href="mailto: client@oschina.cn"><i class='iconfont icon-msg-mail'></i>
<span id='git-footer-email'>client#oschina.cn</span>
</a></div>
<div class='item tel'>
<a class='icon-popup' title='Contact'>
<i class='iconfont icon-tel'></i>
<span>Enterprise:400-606-0201</span>
</a>
</div>
<div class='item tel'>
<a class='d-flex icon-popup' title='Contact'>
<i class='iconfont icon-tel mt-05 mr-05'></i>
<span>Pro：</span>
<div>
13670252304
<br>
13352947997
</div>
</a>
</div>
</div>
</div>
</div>
</div>
</div>
<div class='bottombar'>
<div class='ui container'>
<div class='ui d-flex d-flex-between'>
<div class='seven wide column partner d-flex'>
<div class='open-atom d-flex-center'>
<img class="logo-openatom mr-1" alt="开放原子开源基金会" src="https://cn-assets.gitee.com/assets/logo-openatom-new-955174a984c899d2e230d052bdc237cf.svg" />
<a target="_blank" rel="nofollow" href="https://www.openatom.org/">OpenAtom Foundation</a>
<div class='sub-title ml-1'>Cooperative code hosting platform</div>
</div>
<div class='report-12377 d-flex-center ml-3'>
<img class="report-12377__logo mr-1" alt="违法和不良信息举报中心" src="https://cn-assets.gitee.com/assets/12377@2x-1aa42ed2d2256f82a61ecf57be1ec244.png" />
<a target="_blank" rel="nofollow" href="https://12377.cn">违法和不良信息举报中心</a>
</div>
<div class='copyright ml-3'>
<a rel="nofollow" href="http://beian.miit.gov.cn/">京ICP备2025119063号</a>
</div>
</div>
<div class='nine wide column right aligned'>
<i class='icon world'></i>
<a href="/language/zh-CN">简 体</a>
/
<a href="/language/zh-TW">繁 體</a>
/
<a href="/language/en">English</a>
</div>
</div>
</div>
</div>
</footer>

<script>
  var officialEmail = $('#git-footer-email').text()
  $('#git-footer-main .icon-popup').popup({ position: 'bottom center' })
  $('#git-footer-email').text(officialEmail.replace('#', '@'))
  window.gon.popover_card_locale = {
    follow:"Follow",
    unfollow:"Following",
    gvp_title: "GVP - Gitee Most Valuable Project",
    project: "The author of ",
    org: "The member of ",
    member: "",
    author: "",
    user_blocked: "This account has been blocked or destroyed",
    net_error: "Network error ",
    unknown_exception: "Unknown exception"
  }
  window.gon.select_message = {
    placeholder: "Please enter Gitee Profile Address or email address"
  }
</script>
<script src="https://cn-assets.gitee.com/webpacks/popover_card-01f0ffe9e9806eb10bcd.bundle.js"></script>
<link rel="stylesheet" media="all" href="https://cn-assets.gitee.com/webpacks/css/gitee_nps-ae0dbee40f6ddc72015a.css" />
<script src="https://cn-assets.gitee.com/webpacks/gitee_nps-30c2a3673b61c539fcf7.bundle.js"></script>
<script src="https://cn-assets.gitee.com/webpacks/gitee_icons-0340f9dc8fc1dfbb9937.bundle.js"></script>



<div class='side-toolbar'>
<div class='button toolbar-help'>
<i class='iconfont icon-help'></i>
</div>
<div class='ui popup left center dark'>Going to Help Center</div>
<div class='toolbar-help-dialog'>
<div class='toolbar-dialog-header'>
<h3 class='toolbar-dialog-title'>Search</h3>
<form class="toolbar-help-search-form" action="/help/load_keywords_data" accept-charset="UTF-8" method="get"><input name="utf8" type="hidden" value="&#x2713;" />
<div class='ui icon input fluid toolbar-help-search'>
<input name='keywords' placeholder='Please enter a question' type='text'>
<i class='icon search'></i>
</div>
</form>

<i class='iconfont icon-close toolbar-dialog-close-icon'></i>
</div>
<div class='toolbar-dialog-content'>
<div class='toolbar-help-hot-search'>
<div class='toolbar-roll'>
<a class="init active" title="Git 命令在线学习" href="https://oschina.gitee.io/learn-git-branching/?utm_source==gitee-help-widget"><i class='Blue icon icon-command iconfont'></i>
<span>Git 命令在线学习</span>
</a><a class="init " title="如何在 Gitee 导入 GitHub 仓库" href="https://gitee.com/help/articles/4261?utm_source==gitee-help-widget"><i class='icon icon-clipboard iconfont orange'></i>
<span>如何在 Gitee 导入 GitHub 仓库</span>
</a></div>
<div class='toolbar-list'>
<div class='toolbar-list-item'>
<a href="/help/articles/4114">Git 仓库基础操作</a>
</div>
<div class='toolbar-list-item'>
<a href="/help/articles/4166">企业版和社区版功能对比</a>
</div>
<div class='toolbar-list-item'>
<a href="/help/articles/4191">SSH 公钥设置</a>
</div>
<div class='toolbar-list-item'>
<a href="/help/articles/4194">如何处理代码冲突</a>
</div>
<div class='toolbar-list-item'>
<a href="/help/articles/4232">仓库体积过大，如何减小？</a>
</div>
<div class='toolbar-list-item'>
<a href="/help/articles/4279">如何找回被删除的仓库数据</a>
</div>
<div class='toolbar-list-item'>
<a href="/help/articles/4283">Gitee 产品配额说明</a>
</div>
<div class='toolbar-list-item'>
<a href="/help/articles/4284">GitHub仓库快速导入Gitee及同步更新</a>
</div>
<div class='toolbar-list-item'>
<a href="/help/articles/4328">什么是 Release（发行版）</a>
</div>
<div class='toolbar-list-item'>
<a href="/help/articles/4354">将 PHP 项目自动发布到 packagist.org</a>
</div>
</div>
</div>
<div class='toolbar-help-search-reseult'></div>
</div>
</div>
<script>
  var opt = { position: 'left center'};
  var $helpSideToolbar = $('.button.toolbar-help');
  var $toolbarRoll = $('.toolbar-roll');
  
  $(function() {
    if (false) {
      $helpSideToolbar.popup(opt).popup({lastResort:'left center'})
    } else {
      $helpSideToolbar.popup({lastResort:'left center'}).popup('show', opt);
      setTimeout(function() {
        $helpSideToolbar.popup('hide', opt);
      }, 3000);
    }
  
    if ($toolbarRoll.length) {
      setInterval(function() {
        var $nextActiveLink = $toolbarRoll.find('a.active').next();
        if (!$nextActiveLink.length) {
          $nextActiveLink = $toolbarRoll.find('a:first-child');
        }
        $nextActiveLink.attr('class', 'active').siblings().removeClass('active init');
      }, 5000);
    }
  })
</script>

<div class='popup button' id='home-comment'>
<i class='iconfont icon-comment'></i>
</div>
<div class='ui popup dark'>Comment</div>
<div class='toolbar-appeal popup button'>
<i class='iconfont icon-report'></i>
</div>
<div class='ui popup dark'>
Repository Report
</div>
<script>
  $('.toolbar-appeal').popup({ position: 'left center' });
</script>

<div class='button gotop popup' id='gotop'>
<i class='iconfont icon-top'></i>
</div>
<div class='ui popup dark'>Back to the top</div>
</div>
<div class='form modal normal-modal tiny ui' id='unlanding-complaint-modal'>
<i class='iconfont icon-close close'></i>
<div class='header'>
Login prompt
</div>
<div class='container actions'>
<div class='content'>
This operation requires login to the code cloud account. Please log in before operating.
</div>
<div class='ui orange icon large button ok'>
Go to login
</div>
<div class='ui button blank cancel'>
No account. Register
</div>
</div>
</div>
<script>
  var $elm = $('.toolbar-appeal');
  
  $elm.on('click', function() {
    var modals = $("#unlanding-complaint-modal.normal-modal");
    if (modals.length > 1) {
      modals.eq(0).modal('show');
    } else {
      modals.modal('show');
    }
  })
  $("#unlanding-complaint-modal.normal-modal").modal({
    onDeny: function() {
      window.location.href = "/signup?from=";
    },
    onApprove: function() {
      window.location.href = "/login?from=";
    }
  })
</script>

<style>
  .side-toolbar .bdsharebuttonbox a {
    font-size: 24px;
    color: white !important;
    opacity: 0.9;
    margin: 6px 6px 0px 6px;
    background-image: none;
    text-indent: 0;
    height: auto;
    width: auto;
  }
</style>
<style>
  #udesk_btn a {
    margin: 0px 20px 167px 0px !important;
  }
</style>
<script>
  (function() {
    $('#project-user-message').popup({
      position: 'left center'
    });
  
  }).call(this);
</script>
<script>
  Gitee.initSideToolbar({
    hasComment: true,
    commentUrl: '/yooome/golang#tree_comm_title'
  })
</script>





<script>
  (function() {
    this.__gac = {
      domain: 'www.oschina.net'
    };
  
  }).call(this);
</script>

<script src="https://cn-assets.gitee.com/webpacks/build_status-7effc7b22ddf8e90b34c.bundle.js"></script>
<script src="https://cn-assets.gitee.com/webpacks/scan_status-d44cdcb20ae16410554f.bundle.js"></script>
<script src="https://cn-assets.gitee.com/webpacks/mermaid_render-356b870bb093a31ce9d8.bundle.js"></script>
<script src="https://cn-assets.gitee.com/webpacks/check_runs-19ec228348982570119a.bundle.js"></script>
</body>
</html>

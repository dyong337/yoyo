* [小程序帐号](https://mp.weixin.qq.com/wxopen/initprofile?action=home&lang=zh_CN&token=837925189)

* [小程序没有授权时的处理方法](http://blog.csdn.net/a49220824/article/details/73662360)
* [微信小程序自定义对话框+弹出和隐藏动画详解](http://blog.csdn.net/pcaxb/article/details/56276180)
* [【微信小程序】实现属于自己的美美哒弹窗](http://blog.csdn.net/m549393829/article/details/77996153)
##app.js
	
		const openIdUrl = require('./config').openIdUrl
		
		App({
			//全局变量
			 globalData: {
			    hasLogin: false,
			    openid: null
			  },
			
			  // lazy loading openid
			  getUserOpenId: function(callback) {
			    var self = this
			
			    if (self.globalData.openid) {
			      callback(null, self.globalData.openid)
			    } else {
			      wx.login({
			        success: function(data) {
			          wx.request({
			            url: openIdUrl,
			            data: {
			              code: data.code
			            },
			            success: function(res) {
			              console.log('拉取openid成功', res)
			              self.globalData.openid = res.data.openid
			              callback(null, self.globalData.openid)
			            },
			            fail: function(res) {
			              console.log('拉取用户openid失败，将无法正常使用开放接口等服务', res)
			              callback(res)
			            }
			          })
			        },
			        fail: function(err) {
			          console.log('wx.login 接口调用失败，将无法正常使用开放接口等服务', err)
			          callback(err)
			        }
			      })
			    }
		})

###登录

###代码页面跳转
		
		wx.navigateTo({
	      url: '../logs/logs'
	    })

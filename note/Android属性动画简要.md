###Android属性动画简要
* ##工作原理:
	> 在一定时间间隔内,通过不断对值进行改变，并不断将该值赋值给对对象的属性，从而实现该对象在该属性上的动画效果
* ##工作逻辑
	> ![逻辑图片](/2018-02/images/Property_Animation.png)

* ##ValueAnimator
	1. 定义: 属性动画机制中*最核心*的一个类
	2. 实现动画原理:通过不断控制 值 的变化，再不断 手动 赋给对象的属性，从而实现动画效果。如图下：
		> ![ValueAnimator工作原理](/2018-02/images/ValueAnimator.png)
	3. 实现
		1. Java代码实现
			1. 步骤1：创建动画实例ValueAnimator,并设置初始值和结束值
				> ValueAnimator anim = ValueAnimator.ofInt(0,3);
			2. 步骤2: 设置动画的播放各种属性
				> anim.setDuration(500);  
				> // 设置动画运行的时长  
				> anim.setStartDelay(500);  
        		> // 设置动画延迟播放时间  
        		> anim.setRepeatCount(0);  
        		> // 设置动画重复播放次数 = 重放次数+1  
        		> // 动画播放次数 = infinite时,动画无限重复 
        		> anim.setRepeatMode(ValueAnimator.RESTART);  
        		> // 设置重复播放动画模式  
        		> // ValueAnimator.RESTART(默认):正序重放  
        		> // ValueAnimator.REVERSE:倒序回放  
        	3. 步骤3: 将改变的值手动赋值给对象的属性值：通过动画的更新监听器
        		> // 设置 值的更新监听器  
				> // 即：值每次改变、变化一次,该方法就会被调用一次   
				> `anim.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {}`
			4. 步骤3：将该改变后的赋值给对象的属性值
				> 覆写ValueAnimator.AnimatorUpdateListener的onAnimationUpdate方法  
				> //获取改变后的值  
				> `int curretnValue = (Integer)animation.getAnimatedValue();`
			5. 步骤5: 刷新视图，即重新绘制，从而实现动画效果
				`view.setProperty（currentValue）；`//Property对应属性名称
			6. 步骤6： 启动动画
				`anim.start();`
		2. xml代码实现： 
			1. 创建文件:在文件res/animator/xxx_animation.xml
			2. 设置动画参数 
				> android:valueFrom="0"   // 初始值  
				> android:valueTo="100"  // 结束值  
				> android:valueType="intType" // 变化值类型 ：floatType & intType  
				> android:duration="3000" // 动画持续时间（ms），必须设置，动画才有效果
				> android:startOffset ="1000" // 动画延迟开始时间（ms）  
			    android:fillBefore = “true” // 动画播放完后，视图是否会停留在动画开始的状态，默认为true  
			    android:fillAfter = “false” // 动画播放完后，视图是否会停留在动画结束的状态，优先于fillBefore值，默认为false  
			    android:fillEnabled= “true” // 是否应用fillBefore值，对fillAfter值无影响，默认为true  
			    android:repeatMode= “restart” // 选择重复播放动画模式，restart代表正序重放，reverse代表倒序回放，默认为restart|  
			    android:repeatCount = “0” // 重放次数（所以动画的播放次数=重放次数+1），为infinite时无限重复  
			    android:interpolator = @[package:]anim/interpolator_resource // 插值器，即影响动画的播放速度,下面会详细讲  
			3. 在Java代码中启动动画
				> Animator animator = AnimatorInflater.loadAnimator(context, R.animator.set_animation);
				> animator.setTarget(view);  
				> animator.start();  
* ##ObjectAnimator
	* 直接对对象的属性值进行改变操作，从而实现动画效果
	* 继承自ValueAnimator类，即底层的动画实现机制是基于ValueAnimator类
	* 本质原理： 通过不断控制 值 的变化，再不断 自动 赋给对象的属性，从而实现动画效果。
	* 具体使用:
		> ObjectAnimator animator = ObjectAnimator.ofFloat(mButton, "scaleX", 1f, 3f, 1f);  
		> animator.setDuration(5000);  
		>  animator.start();
	* 属性值说明:
		> ObjectAnimator类根据传入的属性名 去寻找 该对象对应属性名的 set（） & get（）方法，从而进行对象属性值的赋值
* ##TypeEvaluator（估值器）
	* ValueAnimator.ofInt()、ValueAnimator.ofFloat()有系统默认的估值器，ValueAnimator.ofObject()没有; 
	* 自定义TypeEvaluator
		> 1. 实现TypeEvaluator接口
		> 2. 实现evaluate(float fraction, Object startValue, Object endValue)方法(实现估值的逻辑) 
		> 参数说明,fraction-动画完成度，startValue-初始值，endValue-结束值
		> 3. 初始值 过渡 到结束值 的算法是：
		>> 1. 用结束值减去初始值，算出它们之间的差值
		>> 2. 用上述差值乘以fraction系数
		>> 3. 再加上初始值，就得到当前动画的值
* ##组合动画（AnimatorSet 类）

* ##Interpolator (插值器)
	* Java代码:
		> 1. 步骤1：设置需要组合的动画效果
			> `ObjectAnimator  translation = ObjectAnimator.ofFloat(mButton, "translationX", curTranslationX, 300,curTranslationX);`
			> `ObjectAnimator rotate = ObjectAnimator.ofFloat(mButton, "rotation", 0f, 360f);  `   
			> `ObjectAnimator alpha = ObjectAnimator.ofFloat(mButton, "alpha", 1f, 0f, 1f); `
		> 2. 步骤2：创建组合动画的对象
			> `AnimatorSet animSet = new AnimatorSet();  `
		> 3. 步骤3：根据需求组合动画
			> `animSet.play(translation).with(rotate).before(alpha);  ` 
		> 4. 步骤4：启动动画
			> `animSet.start();`
	* xml代码：
		* 1. 创建文件res/animator/set_xxx.xml
		* 2. <set android:ordering="sequentially(按顺序)|together(同时进行)">
		* 3.代码
			 > `AnimatorSet animator = (AnimatorSet) AnimatorInflater.loadAnimator(this, R.animator.set_animation);`
	 		`animator.setTarget(mButton);`  
			`animator.start();`

* ##ViewPropertyAnimator类
	1. 说明：可认为是属性动画的一种简写方式，View.animate().xxx().xxx();
	2. 使用：
		>      mButton.animate().alpha(0f);
		>      mButton.animate().alpha(0f).setDuration(5000).setInterpolator(new BounceInterpolator());
		>      mButton.animate().alpha(0f).x(500).y(500);
	3. 特别说明：
		> 1. 动画自动启动,无需调用start()方法.因为新的接口中使用了隐式启动动画的功能，只要我们将动画定义完成后，动画就会自动启动
		> 2. 该机制对于组合动画也同样有效，只要不断地连缀新的方法，那么动画就不会立刻执行，等到所有在ViewPropertyAnimator上设置的方法都执行完毕后，动画就会自动启动
		> 3. 如果不想使用这一默认机制，也可以显式地调用start()方法来启动动画

* ##监听动画
	* Animation.addListener(new AnimatorListener(){});
	* 动画适配器AnimatorListenerAdapter   
		> new AnimatorListenerAdapter()
		 
* ##总结
	> ![总结](/2018-02/images/zongjie.png)
* 
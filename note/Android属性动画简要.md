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

* ##[补间动画]
[补间动画]:https://www.jianshu.com/p/733532041f46
* 应用场景
	1. Activity 的切换效果  
	 	1. 启动动画
			> Intent intent = new Intent (this,Acvtivity.class);     
			> startActivity(intent);  
			> overridePendingTransition(R.anim.enter_anim,R.anim.exit_anim);  
			> // 采用overridePendingTransition（int enterAnim, int exitAnim）进行设置  
			> // enterAnim：从Activity a跳转到Activity b，进入b时的动画效果资源ID
			> // exitAnim：从Activity a跳转到Activity b，离开a时的动画效果资源Id  
			> // 特别注意  
			> // overridePendingTransition（）必须要在startActivity(intent)后被调用才能生效
		2. 退出动画
			>  finish();  
			>  overridePendingTransition(R.anim.enter_anim,R.anim.exit_anim);  
			>  // 采用overridePendingTransition（int enterAnim, int exitAnim）进行设置  
			>  // enterAnim：从Activity a跳转到Activity b，进入b时的动画效果资源ID  
			>  // exitAnim：从Activity a跳转到Activity b，离开a时的动画效果资源Id  
			>  // 特别注意  
			>  // overridePendingTransition（）必须要在finish()后被调用才能生效  
		3. 系统自带动画
			>  Intent intent = new Intent(MainActivity.this, SecActivity.class);  
			>  startActivity(intent);  
			>  // 淡入淡出的动画效果      
			>  overridePendingTransition(android.R.anim.fade_in, android.R.anim.fade_out);  
			>  // 从左向右滑动的效果   
			>  overridePendingTransition(android.R.anim.slide_in_left, android.R.anim.slide_out_right);
		4. 自定义动画
	2. Fragment动画切换效果
		1. 系统自带的动画切换效果
			>  FragmentTransaction fragmentTransaction = mFragmentManager.beginTransaction();  
			>  fragmentTransaction.setTransition(int transit)；  
			>  通过setTransition(int transit)进行设置  
			>  transit参数说明  
			>  1. FragmentTransaction.TRANSIT_NONE：无动画  
			>  2. FragmentTransaction.TRANSIT_FRAGMENT_OPEN：标准的打开动画效果    
			>  标准动画设置好后，在Fragment添加和移除的时候都会有。 
		2. 自定义动画效果  
			> FragmentTransaction fragmentTransaction = mFragmentManager
                .beginTransaction();
			> fragmentTransaction.setCustomAnimations(R.anim.in_from_right, R.anim.out_to_left);
			> 此处的自定义动画效果同Activity，此处不再过多描述
	3. 视图组（ViewGroup）中子元素的出场效果
		1. 设置子元素的出场动画res/anim/view_animation.xml
		2. 设置 视图组（ViewGroup）的动画文件res/ anim /anim_layout.xml
			
			<?xml version="1.0" encoding="utf-8"?>
			// 采用LayoutAnimation标签
			<layoutAnimation xmlns:android="http://schemas.android.com/apk/res/android"
			    android:delay="0.5"
			    // 子元素开始动画的时间延迟
			    // 如子元素入场动画的时间总长设置为300ms
			    // 那么 delay = "0.5" 表示每个子元素都会延迟150ms才会播放动画效果
			    // 第一个子元素延迟150ms播放入场效果；第二个延迟300ms，以此类推
			
			    android:animationOrder="normal"
			    // 表示子元素动画的顺序
			    // 可设置属性为：
			    // 1. normal ：顺序显示，即排在前面的子元素先播放入场动画
			    // 2. reverse：倒序显示，即排在后面的子元素先播放入场动画
			    // 3. random：随机播放入场动画
			
			    android:animation="@anim/view_animation"
			    // 设置入场的具体动画效果
			    // 将步骤1的子元素出场动画设置到这里
		
			    />
		3. 为视图组（ViewGroup）指定andorid:layoutAnimation属性
			1. xml  
									
					<?xml version="1.0" encoding="utf-8"?>
					<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
					    xmlns:tools="http://schemas.android.com/tools"
					    android:layout_width="match_parent"
					    android:layout_height="match_parent"
					    android:background="#FFFFFF"
					    android:orientation="vertical" >
					    <ListView
					        android:id="@+id/listView1"
					        android:layoutAnimation="@anim/anim_layout"
					        // 指定layoutAnimation属性用以指定子元素的入场动画
					        android:layout_width="match_parent"
					        android:layout_height="match_parent" />
					</LinearLayout>
			2. 在Java代码中指定
				
					ListView lv = (ListView) findViewById(R.id.listView1);
			        Animation animation = AnimationUtils.loadAnimation(this,R.anim.anim_item);
			         // 加载子元素的出场动画
			        LayoutAnimationController controller = new LayoutAnimationController(animation);
			        controller.setDelay(0.5f);    
			        controller.setOrder(LayoutAnimationController.ORDER_NORMAL);    
				    // 设置LayoutAnimation的属性  
				    lv.setLayoutAnimation(controller); 
				    // 为ListView设置LayoutAnimation的属性

## 逐帧动画
* 原理
	* 将动画拆分为 帧 的形式，且定义每一帧 = 每一张图片
	* 逐帧动画的本质：按序播放一组预先定义好的图片
* 具体使用 
	1. 将动画资源（即每张图片资源）放到 drawable文件夹里
		
			技巧：
				找到自己需要的gif动画
				用 gif分解软件（如 GifSplitter）将 gif 分解成一张张图片即可
	2. 设置 & 启动 动画
		1. XML实现
			1. 在 res/anim的文件夹里创建动画效果.xml文件
			2. 步骤2：设置动画资源（图片资源)knight_attack.xml
				
					<?xml version="1.0" encoding="utf-8"?>
					<animation-list
					    xmlns:android="http://schemas.android.com/apk/res/android"
					    android:oneshot="true" // 设置是否只播放一次，默认为false>

						// item = 动画图片资源；duration = 设置一帧持续时间(ms)
					    <item android:drawable="@drawable/a0" android:duration="100"/>
					    <item android:drawable="@drawable/a1" android:duration="100"/>
					    <item android:drawable="@drawable/a2" android:duration="100"/>
					    <item android:drawable="@drawable/a3" android:duration="100"/>
					    <item android:drawable="@drawable/a4" android:duration="100"/>
					    <item android:drawable="@drawable/a5" android:duration="100"/>
					    <item android:drawable="@drawable/a6" android:duration="100"/>
					    <item android:drawable="@drawable/a7" android:duration="100"/>
					    <item android:drawable="@drawable/a8" android:duration="100"/>
					    <item android:drawable="@drawable/a9" android:duration="100"/>
					    <item android:drawable="@drawable/a10" android:duration="100"/>
					    <item android:drawable="@drawable/a11" android:duration="100"/>
					    <item android:drawable="@drawable/a12" android:duration="100"/>
					    <item android:drawable="@drawable/a13" android:duration="100"/>
					    <item android:drawable="@drawable/a14" android:duration="100"/>
					    <item android:drawable="@drawable/a15" android:duration="100"/>
					    <item android:drawable="@drawable/a16" android:duration="100"/>
					    <item android:drawable="@drawable/a17" android:duration="100"/>
					    <item android:drawable="@drawable/a18" android:duration="100"/>
					    <item android:drawable="@drawable/a19" android:duration="100"/>
					    <item android:drawable="@drawable/a20" android:duration="100"/>
					    <item android:drawable="@drawable/a21" android:duration="100"/>
					    <item android:drawable="@drawable/a22" android:duration="100"/>
					    <item android:drawable="@drawable/a23" android:duration="100"/>
					    <item android:drawable="@drawable/a24" android:duration="100"/>
					    <item android:drawable="@drawable/a25" android:duration="100"/>
					</animation-list>
			3.  在Java代码中载入 & 启动动画
		
					// 1. 设置动画
					iv.setImageResource(R.drawable.knight_attack);
					// 2. 获取动画对象
	 				AnimationDrawable animationDrawable = (AnimationDrawable) iv.getDrawable();
					// 3. 启动动画
					animationDrawable.start();
		2. Java代码实现
			
				AnimationDrawable animationDrawable = new AnimationDrawable();
		        for (int i = 0; i <= 25; i++) {
		            int id = getResources().getIdentifier("a" + i, "drawable", getPackageName());
		            Drawable drawable = getResources().getDrawable(id);
		            animationDrawable.addFrame(drawable, 100);
		        }
				animationDrawable.setOneShot(true);
 				iv.setImageDrawable(animationDrawable);
				animationDrawable.stop();
				// 特别注意：在动画start()之前要先stop()，不然在第一次动画之后会停在最后一帧，这样动画就只会触发一次
				animationDrawable.start();
* 特点
	* 优点：使用简单、方便
	* 缺点：容易引起 OOM，因为会使用大量 & 尺寸较大的图片资源
		> 尽量避免使用尺寸较大的图片
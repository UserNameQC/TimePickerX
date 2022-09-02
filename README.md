## 借用原项目，更改为AndroidX后重新上传的。
## 原项目地址：https://github.com/Bigkoo/Android-PickerView

## Android-PickerView
[![API](https://img.shields.io/badge/API-9%2B-brightgreen.svg)](https://android-arsenal.com/api?level=9) 
[![License](https://img.shields.io/badge/license-Apache%202-green.svg)](https://www.apache.org/licenses/LICENSE-2.0)
[![Download](https://api.bintray.com/packages/contrarywind/maven/Android-PickerView/images/download.svg) ](https://bintray.com/contrarywind/maven/Android-PickerView/_latestVersion)

[![GitHub stars](https://img.shields.io/github/stars/Bigkoo/Android-PickerView.svg?style=social)](https://github.com/Bigkoo/Android-PickerView/stargazers) [![GitHub forks](https://img.shields.io/github/forks/Bigkoo/Android-PickerView.svg?style=social)](https://github.com/Bigkoo/Android-PickerView/network) [![GitHub watchers](https://img.shields.io/github/watchers/Bigkoo/Android-PickerView.svg?style=social)](https://github.com/Bigkoo/Android-PickerView/watchers)




## 介绍

具体使用请去原项目下查看，方法都一样，依赖更改一下即可。


### 使用注意事项
* 注意：当我们进行设置时间的启始位置时，需要特别注意月份的设定
* 原因：Calendar组件内部的月份，是从0开始的，即0-11代表1-12月份
* 错误使用案例： 
  startDate.set(2013,1,1);
  endDate.set(2020,12,1);
* 正确使用案例：
  startDate.set(2013,0,1);
  endDate.set(2020,11,1);


### **如何使用：**

#### Android-PickerView 库使用示例：

#### 1.添加Jcenter仓库 Gradle依赖：
```java
implementation 'com.github.UserNameQC:TimePickerX:0.0.0'
```

#### 2.在项目中添加如下代码：

```java
//时间选择器
TimePickerView pvTime = new TimePickerBuilder(MainActivity.this, new OnTimeSelectListener() {
                           @Override
                           public void onTimeSelect(Date date, View v) {
                               Toast.makeText(MainActivity.this, getTime(date), Toast.LENGTH_SHORT).show();
                           }
                       }).build();
```

```java
//条件选择器
 OptionsPickerView pvOptions = new OptionsPickerBuilder(MainActivity.this, new OnOptionsSelectListener() {
            @Override
            public void onOptionsSelect(int options1, int option2, int options3 ,View v) {
                //返回的分别是三个级别的选中位置
                String tx = options1Items.get(options1).getPickerViewText()
                        + options2Items.get(options1).get(option2)
                        + options3Items.get(options1).get(option2).get(options3).getPickerViewText();
                tvOptions.setText(tx);
            }
        }).build();
 pvOptions.setPicker(options1Items, options2Items, options3Items);
 pvOptions.show(); 
```
#### 大功告成~

#### 3.如果默认样式不符合你的口味，可以自定义各种属性：
```java
 Calendar selectedDate = Calendar.getInstance();
 Calendar startDate = Calendar.getInstance();
 //startDate.set(2013,1,1);
 Calendar endDate = Calendar.getInstance();
 //endDate.set(2020,1,1);
 
  //正确设置方式 原因：注意事项有说明
  startDate.set(2013,0,1);
  endDate.set(2020,11,31);

 pvTime = new TimePickerBuilder(this, new OnTimeSelectListener() {
            @Override
            public void onTimeSelect(Date date,View v) {//选中事件回调
                tvTime.setText(getTime(date));
            }
        })
                .setType(new boolean[]{true, true, true, true, true, true})// 默认全部显示
                .setCancelText("Cancel")//取消按钮文字
                .setSubmitText("Sure")//确认按钮文字
                .setContentSize(18)//滚轮文字大小
                .setTitleSize(20)//标题文字大小
                .setTitleText("Title")//标题文字
                .setOutSideCancelable(false)//点击屏幕，点在控件外部范围时，是否取消显示
                .isCyclic(true)//是否循环滚动
                .setTitleColor(Color.BLACK)//标题文字颜色
                .setSubmitColor(Color.BLUE)//确定按钮文字颜色
                .setCancelColor(Color.BLUE)//取消按钮文字颜色
                .setTitleBgColor(0xFF666666)//标题背景颜色 Night mode
                .setBgColor(0xFF333333)//滚轮背景颜色 Night mode
                .setDate(selectedDate)// 如果不设置的话，默认是系统时间*/
                .setRangDate(startDate,endDate)//起始终止年月日设定
                .setLabel("年","月","日","时","分","秒")//默认设置为年月日时分秒
                .isCenterLabel(false) //是否只显示中间选中项的label文字，false则每项item全部都带有label。
                .isDialog(true)//是否显示为对话框样式
                .build();
```

```java
pvOptions = new  OptionsPickerBuilder(this, new OptionsPickerView.OnOptionsSelectListener() {
            @Override
            public void onOptionsSelect(int options1, int option2, int options3 ,View v) {
                //返回的分别是三个级别的选中位置
                String tx = options1Items.get(options1).getPickerViewText()
                        + options2Items.get(options1).get(option2)
                        + options3Items.get(options1).get(option2).get(options3).getPickerViewText();
                tvOptions.setText(tx);
            }
        }) .setOptionsSelectChangeListener(new OnOptionsSelectChangeListener() {
                              @Override
                              public void onOptionsSelectChanged(int options1, int options2, int options3) {
                                  String str = "options1: " + options1 + "\noptions2: " + options2 + "\noptions3: " + options3;
                                  Toast.makeText(MainActivity.this, str, Toast.LENGTH_SHORT).show();
                              }
                          })
                .setSubmitText("确定")//确定按钮文字
                .setCancelText("取消")//取消按钮文字
                .setTitleText("城市选择")//标题
                .setSubCalSize(18)//确定和取消文字大小
                .setTitleSize(20)//标题文字大小
                .setTitleColor(Color.BLACK)//标题文字颜色
                .setSubmitColor(Color.BLUE)//确定按钮文字颜色
                .setCancelColor(Color.BLUE)//取消按钮文字颜色
                .setTitleBgColor(0xFF333333)//标题背景颜色 Night mode
                .setBgColor(0xFF000000)//滚轮背景颜色 Night mode
                .setContentTextSize(18)//滚轮文字大小
                .setLinkage(false)//设置是否联动，默认true
                .setLabels("省", "市", "区")//设置选择的三级单位
                .isCenterLabel(false) //是否只显示中间选中项的label文字，false则每项item全部都带有label。
                .setCyclic(false, false, false)//循环与否
                .setSelectOptions(1, 1, 1)  //设置默认选中项
                .setOutSideCancelable(false)//点击外部dismiss default true
                .isDialog(true)//是否显示为对话框样式
                .isRestoreItem(true)//切换时是否还原，设置默认选中第一项。
                .build();

        pvOptions.setPicker(options1Items, options2Items, options3Items);//添加数据源
```
#### 4.如果需要自定义布局：

```java
        // 注意：自定义布局中，id为 optionspicker 或者 timepicker 的布局以及其子控件必须要有，否则会报空指针
        // 具体可参考demo 里面的两个自定义布局
        pvCustomOptions = new OptionsPickerBuilder(this, new OptionsPickerView.OnOptionsSelectListener() {
            @Override
            public void onOptionsSelect(int options1, int option2, int options3, View v) {
                //返回的分别是三个级别的选中位置
                String tx = cardItem.get(options1).getPickerViewText();
                btn_CustomOptions.setText(tx);
            }
        })
                .setLayoutRes(R.layout.pickerview_custom_options, new CustomListener() {
                    @Override
                    public void customLayout(View v) {
                        //自定义布局中的控件初始化及事件处理
                        final TextView tvSubmit = (TextView) v.findViewById(R.id.tv_finish);
                        final TextView tvAdd = (TextView) v.findViewById(R.id.tv_add);
                        ImageView ivCancel = (ImageView) v.findViewById(R.id.iv_cancel);
                        tvSubmit.setOnClickListener(new View.OnClickListener() {
                            @Override
                            public void onClick(View v) {
                                pvCustomOptions.returnData(tvSubmit);
                            }
                        });
                        ivCancel.setOnClickListener(new View.OnClickListener() {
                            @Override
                            public void onClick(View v) {
                                pvCustomOptions.dismiss();
                            }
                        });

                        tvAdd.setOnClickListener(new View.OnClickListener() {
                            @Override
                            public void onClick(View v) {
                                getData();
                                pvCustomOptions.setPicker(cardItem);
                            }
                        });

                    }
                })
                .build();
        pvCustomOptions.setPicker(cardItem);//添加数据
```

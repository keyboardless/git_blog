---
title: trie tree
date: 2016-08-16 13:31:21
tags:
---

# 双数组Trie数
[An Implementation of Double-Array Trie](https://linux.thai.net/~thep/datrie/datrie.html)
一个蛮详细的从三数组、两数组原理介绍，暂时还没有看明白
[双数组Trie树(DoubleArrayTrie)Java实现](http://www.hankcs.com/program/java/%E5%8F%8C%E6%95%B0%E7%BB%84trie%E6%A0%91doublearraytriejava%E5%AE%9E%E7%8E%B0.html)
用了一个日本人实现的库
[The Trie: A Neglected Data Structure](https://www.toptal.com/java/the-trie-a-neglected-data-structure)
about large text search.

# 全文检索
使用了一个lucene的库
[实战 Lucene，第 1 部分: 初识 Lucene](https://www.ibm.com/developerworks/cn/java/j-lo-lucene1/)

# 依存关系
用到一种CoNLL的格式
[汉语树库](http://www.hankcs.com/nlp/corpus/chinese-treebank.html)
这里面介绍第二届自然语言处理与中文计算会议（NLP&CC 2013）中用到的两个语聊，分别是清华的和哈工大的

# Ansj分词
[说明文档](http://nlpchina.github.io/ansj_seg/)

配置文件中有，.map


现在传入recognizeSemantic()的三个参数
String asrContext = "{\"auid\":\"23232342424\",\"uuid\":\"23232424\"}";
String appkey = "lanlan-nlp";
String asrTxt = "打开空调";

多伦对话的历史对话信息，append到asrContext里面，并作为返回的参数

V1：
第一次调用：
asrContext = recognizeSemantic(appkey, asrContext, asrTxt);

asrContext = {"auid":"23232342424","uuid":"23232424", "round1":"{第一轮对话内容}" }
第一轮对话内容 = {"usr":"打开空调", "robo":"{"data":{"Switch":"1","appliance":"AIRCONDITION"},"intent":"smarthome","name":"smarthome"}", "nlp":"哪里的空调"}

第二次调用
asrTxt = "卧室的";
asrContext = recognizeSemantic(appkey, asrContext, asrTxt);

asrContext = {"auid":"23232342424","uuid":"23232424", "round1":"{第一轮对话内容}","round2":"{第二轮对话内容}" }
第一轮对话内容 = {"usr":"打开空调", "robo":"{"data":{"Switch":"1","appliance":"AIRCONDITION"},"intent":"smarthome","name":"smarthome"}", "nlp":"哪里的空调"}
第二轮对话内容 = {"usr":"卧室的","robo":"{"data":{"Switch":"1","appliance":"AIRCONDITION","position":"厨房"},"intent":"smarthome","name":"smarthome"}","nlp":"正在打开卧室的空调"}

第三次调用
asrTxt = "温度打到25度";
asrContext = recognizeSemantic(appkey, asrContext, asrTxt);

asrContext = {"auid":"23232342424","uuid":"23232424", "round1":"{第一轮对话内容}","round2":"{第二轮对话内容}","round3":"{第三轮对话内容}" }

V2：
String asrContext = "{\"auid\":\"23232342424\",\"uuid\":\"23232424\"}";
String appkey = "lanlan-nlp";
String asrTxt = "打开空调";
第一次调用：
asrContext = recognizeSemantic(appkey, asrContext, asrTxt);

返回结果
asrContext = {"auid":"23232342424","uuid":"23232424", "data":"{"Switch":"1","appliance":"AIRCONDITION"}" , ,"intent":"smarthome","name":"smarthome","nlp":"哪里的空调"}

第二次调用：
asrTxt = "卧室的";
asrContext = recognizeSemantic(appkey, asrContext, asrTxt);
返回结果	
asrContext = {"auid":"23232342424","uuid":"23232424", "data":"{"Switch":"1","appliance":"AIRCONDITION","position":"卧室"}" , ,"intent":"smarthome","name":"smarthome","nlp":"正在打开卧室空调"}

第三次调用
asrTxt = "温度打到25度";
asrContext = recognizeSemantic(appkey, asrContext, asrTxt);
返回结果
asrContext = {"auid":"23232342424","uuid":"23232424", "data":"{"Temperature":"25","appliance":"AIRCONDITION",""position:"卧室"}" , ,"intent":"smarthome","name":"smarthome","nlp":"正在设置卧室空调为25度"}






# DM+ 问题

用什么编辑软件 比较方便

可以只有一个step的task？(car_control.xml)，图的起点和终点是同一个？

<Action goto="@end" >Action://DelegateToDevice</Action> 
<Action goto="@end" >Action://Control/BackHome</Action>  这些action在哪里定义，如何真正与设备通信

cache=false  目的 没有太理解

<Output>
    <Sentence type="written">${getPlayMusicLG}</Sentence>
    <Sentence type="spoken">${getPlayMusicLG}</Sentence>
</Output>   这种是取什么值


<Condition func="domain" expected="car_restriction" /> 并不知道domain这个函数返回值的取值集合

grammar com.alibaba.idst.nui.demo;
public <main> = (<music_command>){Domain.music}; 这儿和wiki上写的不太一样

如何调试

打杂，是有事情可做，但是没有长进

{
  "domain":"notify",
  "slots":{
     "days":[],
     "time":[],
     "info":[],
  }
}


赵骥的demo
温度调高低和灯光调亮暗   是否涉及 多个设备？
菜谱对话 要先指定菜名？
{
  "domain":"smarthome_command",
  "slots":{
     "days":[],
     "time":[],
     "info":[],
  }
}

闹钟功能设计
5. 闹钟提醒场景
5.1. Action

Action  Status描述
Action://Alarm/Inform  显示内容，如要展示列表，根据web_action决定
Action://Alarm/Ask  同Confirm，让用户确认，是设置还是取消
Action://Alarm/Confirm  让用户确认，是设置还是取消
Action://Alarm/Set  确定为设置
Action://Alarm/Cancel  确定为取消
Action://Alarm/View  查看闹钟列表
Action://Alarm/Delete  删除某个闹钟
Action://Alarm/Select  从列表中选择
Action://Alarm/Disable  取消闹钟，但不删除
Action://Alarm/Reqmore  同步闹钟列表

领域(domain)  alarm
意图(intent)  set_alarm  设置闹钟
  delete_alarm  删除闹钟设置
  view_alarm  查看闹钟设置
  cancel_alarm  取消闹钟设置
  close_alarm  关闭闹钟
  resume_alarm  回到闹钟
属性(slots)  字段名称  字段类型  字段说明  取值示例
  time  DATETIME  时间  明天
示例：设置明天早上8点钟的闹钟
[
    {
        "domain":"alarm",
        "intent":"set_alarm",
        "score":1,
        "slots":{
            "time":[
                {
                    "error_code":"0",
                    "norm":[
                        "2015-11-25 08:00:00"
                    ],
                    "raw":"明天早上8点钟",
                    "relative_mode":"0",
                    "type":"equal"
                }
            ]
        }
    }
]

赵骥 协议
// 空调
{"domain":"smarthome_command",
 "intent":"temperature_up"  //temperature_down
 "slot":{"temperature":"1"}
 }

 {"domain":"smarthome_command",
 "intent":"temperature_max"  //temperature_min
 "slot":{}
 }

// 灯
 {"domain":"smarthome_command",
 "intent":"luminance_up"  //luminance_down
 "slot":{"brightness":"1"}
 }

{"domain":"smarthome_command",
 "intent":"luminance_max"  //luminance_min
 "slot":{}
 }

// 菜谱
{"domain":"smarthome_command",
 "intent":"cookbook_next"  //cookbook_last,cookbook_start
 "slot":{}
 }

// 闹钟
{"domain":"smarthome_command",
 "intent":"clockalarm"
 "slot":{"time":"...","",spoken_text":"..."}
 }


 {"domain":"smarthome_command",
 "intent":"babysleep"
 "slot":{}
 }

 {"domain":"smarthome_command",
 "intent":"babygetup"
 "slot":{}
 }

 {"domain":"smarthome_command",
 "intent":"babygowork
 "slot":{}
 }

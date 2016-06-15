---
layout: post
title: SpringMVC-参数绑定方式
author: leping
category: Pages
tags: [jekyll, github]
---

## @Requestparam 绑定单个请求的值
 
   url：/requestparam1?username=zhang  
   @RequestMapping("/requestparam1")  
   public String requestparam2(@RequestParam("username") String username)  
 
## @PathVariable 绑定URI模板变量值

  @RequestMapping(value="/users/{userId}/topics/{topicId}")   
  public String test(  
       @PathVariable(value="userId") int userId,   
       @PathVariable(value="topicId") int topicId)  


## @SessionAttributes 绑定命令对象到session
   //1、在控制器类头上添加@SessionAttributes注解  
   @SessionAttributes(value = {"user"})    
   public class SessionAttributeController   
  
   //2、@ModelAttribute注解的方法进行表单引用对象的创建  
   @ModelAttribute("user")    
   public UserModel initUser()   
  
   //3、@RequestMapping注解方法的@ModelAttribute注解的参数进行命令对象的绑定  
   @RequestMapping("/session1")  
   public String session1(@ModelAttribute("user") UserModel user)  
  
   //4、通过SessionStatus的setComplete()方法清除@SessionAttributes指定的会话数据  
   @RequestMapping("/session2")   
   public String session(@ModelAttribute("user") UserModel user, SessionStatus status) {  
    if(true) { //④   
        status.setComplete();    
    }    
    return "success";  
    }  

  
## @Value 绑定从配置文件取值  


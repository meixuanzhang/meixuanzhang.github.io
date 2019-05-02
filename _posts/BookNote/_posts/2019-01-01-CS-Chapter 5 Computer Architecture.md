---
layout: post
title: Chapter 5 Computer Architecture
date:   2019-03-23
categories: ["The Elements Of Computing Systems"]
---
So basically there are, I would say three types of information that's usually passed around the system, and one of them is the data. When we have a number that needs to be added, of course the number needs to be moved from some, from one place to another, from the data in memory to the registers, to the actual other systematic logic unit that's going to do something with them, and back. 

The second type of information that we need to control is what's called addresses. What instruction are we actually executing now? What piece of data within the memory do we need to access now? These are in addresses. 

And, of course, there is going to be a, there is going to be a big bunch of wires that actually do all the control. That actually tell each part of the system what to do at this particular point and this is called the control. Sometimes all these three pieces of the, each one of these pieces of information is actually going to be implemented by wires, by a set of wires sometimes called a bus. 


 the simplest and clearest part of the CPU of our computer. It basically needs to be able to accept numbers. And add them, subtract them. Do some logical operations on them. So it's very simple. We need, simply need to have some information from the databus connect into the ALU. And then information. And then feeds the output value back into the databus. That's going to be a, and from there, of course, it's going to have to go to other places that also connect to the databus, like the memory or the registers.
 
 
 There is one other piece of infor, plus other type of pieces of information that ALB would, ALU will need to be connected to, this is the control bus. On one hand, of course the ALU needs to know what kind of operation it does every time. So it has to reget information from the control bus, specifying the type of operation that it does. And on the other hand, according to the results of the arithmetic or logical operations that it does. It's going to be able to, have to be able to tell the other parts of the system what to do.
 
 The ALU loads information from the Data bus and manipulates it using the Control bits.
 
 
  we store intermediate results in the registers. So we're going to be, have to be able to take data in, from the data bust into the registers and then also take data's from the register then feeds them back into the data bus. And of course where would they go from the data bus to other parts of the system such, as the ALU. So this is the first thing that of course we will have to connect all the registers to the data bus.
  
   some registers are used to specify addresses. The way we actually achieve indirect addressing into a RAM or jump into a ROM address, the way we do it is usually we put numbers, addresses into a register and then that specifies where we want to access

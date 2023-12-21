## Purpose of this page is do document the process of making a T3 app from scratch



First thing I want to do is to make the Auth work with google in this case. 

https://www.youtube.com/watch?v=A5ZN--P9vXM  - reference video 

https://next-auth.js.org/providers/google - Read about the refresh token


<mark style="background: #FF5582A6;">Issues</mark>:

Currently there seems to be an issue with the `rich-markdown-editor` where it renders 2x. I have to figure out why this happens and how to disable it. 

<mark style="background: #BBFABBA6;">Solution</mark> : https://github.com/ueberdosis/tiptap this editor seems to fix this issue

There seems to be an issue with Tiptap and some solutions are here https://github.com/ueberdosis/tiptap/issues/2403 

<mark style="background: #FFF3A3A6;">Will need to investigate more.</mark>

After investigation: Solution was using the tiptap and I had to make it very custom in this regard, a screenshot 
![[Pasted image 20220915141906.png]]

Posted also in the github: https://github.com/ueberdosis/tiptap/issues/2403 

Maybe this warrants a [[blogpost]] ? 

Also I've used the [[Second Brain/🖥️ Coding/Coding/TRPC/TRPC example app]] to understand the flow better. 

Added [[TODO]] stuff which should be worked on. 

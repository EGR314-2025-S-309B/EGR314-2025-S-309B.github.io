## Lessons Learned
Throughout working on this project, there are many key things we learned, both from a technical and professional standpoint, that are important for any engineer. These lessons are listed out below.

1. __Clarifying requirements:__ While working thorugh this project, we learned that having clear constraints and goals is important when planning what visions and ideas you have for a project. Having clear requirements allows you to keep your project on track and results in less backtracking.
2. __Time Management:__ Having good time management and ensuring deadlines are being met is a required part of any project. It is important to always know where you aree at in your project and what goals you need to meet, as well as how much time you have to meet these goals. It can be benificial to have a designated member that is in charge of tracking these deadlines.
3. __Team Collaboration:__ Having solid team cohesion is a major part of having the project as a whole run smoothly. It is important that if you are having issues within your team that you address them appropriately and do not let any issues fester within your group.
4. __Communication:__ Along with collaboration, communication is also important when you are in a team project. Make sure to always express any issues or comments you may have about the project so that you can receive assistance or guidance. This will help when it comes to ensuring you have the best possible results.
5. __Documentation:__ Noting down and taking pictures of your project as you move through the different steps is very important. This allows you to be able to go back and see what works, so when something breaks, you can always replicate your results.
6. __Flexibility:__ Being able to adapt and change your project on the fly is very important. With how fast some aspects of the project can change in the classroom, it is always important to stay updated and be able to make necessary changes as quick as possible.
7. __Testing:__ Testing your project at every stage is necessary, especially when designing PCBs and coding. Verifying what parts of your systems are working individually and when connected with other systems will allow you to track progress better and improve the troubleshooting process.
8. __Learning From Mistakes:__ Being able to learn from mistakes you make during the design process is very important. This allows you to not only improve those mistakes on the current project, but also carry that information on any further projects you may work on for the rest of your career.
9. __Quality Over Speed:__ Especially when deadlines are approach quickly and tensions are high, it can be easy to rush through work and make mistakes. It is important to remember that rushing can cause issues in your project that can be detrimental, so make sure to still double-check all of your work and put quality work forward.
10. __Accepting Feedback:__ When working through any project that has a user or oversight by a teacher or project manager, it is important to be able to take feedback and use it to improve the project. If there is feedback you don't understand or have questions about, make sure to get clarification so you can make the best possible project for the user group.

## Recommendations for Future Students
1.  __Make a folder just for the class/project.__ This will help once you need to find certain files or code when using information from labs and implementing it into your projects.
2.  __Have designated roles in your team.__ This will allow you to keep all members accountable and make sure everyone is participating, as well as making sure no one is falling behind in their duties.
3.  __Utilize help from the teaching team.__ The teachers for the class have been operating the class for years and have seen many of the pitfalls you may fall into while working through the project. Not only that, but the TAs have also taken the class and know the frustrations you may be facing. Communicating with the teaching team often will help you immensely while working through the project.
4.  __Document everything.__ Many issues will pop up as you work through making your system. Make sure to track every step of your project as you work through it so you always have something to refer back to.
5.  __Lastly, learn to take your time.__ Especially in as intensive a class as EGR304/314, it can be easy to become frustrated and make stupid mistakes. Learn to breathe, take a step back, and take a calm and composed approach to whatever issues you may be facing.

## Version 2.0

If we were to make a Version 2.0 of our system, one of the biggest things to fix is the MQTT communication. It mostly works, but it can get kinda sketchy when the Wi-Fi isn’t great or things get busy.

Right now we’re using MQTT to send stuff like spin data to the dashboard. It’s light and fast, which is great, but it can drop stuff or just not send if the connection glitches. In version 2.0, we’d try a few things to make it better. We would definitly make it reconnect by itself if it disconnects. Also having it store messages when it’s offline would be useful. Split the messages into different “topics” for sensor data, motor direction data, etc.

We would also want to add back the gyroscope sensor we were going to use before. This would allow for more control of the top rather than just an on and off. 

Finnaly, some more physical indicators would be useful to show whats happening. Right now, nothing really shows whent he motor is supposed to be on or off or what speed its at. Having audio or led indicators would make it easier to show what the device is trying to do rather than relying on what we think its doing.

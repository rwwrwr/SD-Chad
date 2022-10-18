# SD Chad - Stable Diffusion Aesthetic Scorer

Have been using SD to create art for the last month, finding a template that works across prompt, seed, settings, and then creating 100s of images from it, selecting the best, deleting the rest. 

That flow works great already, have lots of pics that look as good as those trending on ArtStation. Then I thought about automating this using AI. Here is what I have done so far: 

- Got the 10M prompts, seeds, settings, urls from the SD beta discord bot, Aug 2022 (same set used for krea.ai and lexica.art)
https://github.com/krea-ai/open-prompts
- Normalized the data by selecting 548K samples that are 512 x 512, 50 steps, 7 scale, not repeated seeds + prompt combo
https://drive.google.com/file/d/1c4WHxtlzvHYd0UY5WCMJNn2EO-Aiv2A0/view
- Downloaded the images, got image and text embeddings using img2dataset and Clip Retrieval (amazing framework)
https://github.com/rom1504/clip-retrieval
- Ran those images through ASV1 (created by LAION from 4K gens) and ASV2 (created from 250K gens + no gens, used to get the image set that SD was trained on)  
https://github.com/LAION-AI/aesthetic-predictor  
https://github.com/christophschuhmann/improved-aesthetic-predictor
- Created a script for SD, so one can generate images, and depending on score, they get saved in different folders, different file names
https://github.com/grexzen/SD-Chad/blob/main/chad_scorer.py

ASV1 has a nicer distribution of scores, while ASV2 is pretty tight in the middle. Since ASV2 was created by scoring non-gens that might be why is so strict scoring gens from SD. It also seems to prefer realistic images.

![image](https://user-images.githubusercontent.com/30579087/194380290-6c68fb6b-cd78-4d9f-9ff2-bdbe2c3d43bb.png)

Here is ASV1. Album score =10 https://ibb.co/album/cY7GQW. Album score = 0 https://ibb.co/album/84p0Bk.

![image](https://user-images.githubusercontent.com/30579087/194484756-c7458d79-876f-4494-a431-604046efa26b.png)

Here is ASV2. Album score = 8 (highest) https://ibb.co/album/ypWyhL. Album score = 2 (lowest) https://ibb.co/album/0Rk3Yx.

![image](https://user-images.githubusercontent.com/30579087/194484962-d578229c-6c0c-4909-a98f-5fe7b59eb672.png)

Another cool thing is that it seems to be able to score the image similarly as soon as step 1-2, although you only have until about step 10-15 before it becomes another image no matter the sampler used. 

So this could save so much time producing great looking images from the start. We could even set a limit at step 1, then at step x, and so on, so the generation process doesn't waste time on garbage.

Next step is to retrain the scorer using the 548K SD gens. More to come soon.  



# SD Chad - Stable Diffusion Aesthetic Scorer

Have been using SD to create art for the last month, finding a template that works across prompt, seed, settings, and then creating 100s of images from it, selecting the best, deleting the rest. 

That flow works great already, have lots of pics that look as good as those trending on ArtStation. Then I thought about automating this using AI. Here is what I have done so far: 

- Got the 10M prompts, seeds, settings, urls from the SD beta discord bot, Aug 2022 (same set used for lexica.art)
- Normalized the data by selecting 548K samples that are 512 x 512, 50 steps, 7 scale, not repeated seeds + prompt combo
- Downloaded the images, got image and text embeddings using Clip Retrieval 
- Ran those images through ASV1 (created by LAION from 4K gens) and ASV2 (created from 250K gens + no gens, used to get the image set that SD was trained on)

ASV1 has a nicer distribution of scores, while ASV2 is pretty tight in the middle. Since ASV2 was created by scoring non-gens that might be why is so strict scoring gens from SD. It also seems to prefer realistic images.

![image](https://user-images.githubusercontent.com/30579087/194380290-6c68fb6b-cd78-4d9f-9ff2-bdbe2c3d43bb.png)

Both seem to be off scoring gen images. 

Here is ASV1. Album score =10 https://ibb.co/album/VVmW2Y. Album score = 0 https://ibb.co/album/dGS1RQ.

![image](https://user-images.githubusercontent.com/30579087/194382366-8ae204fa-c65c-44a6-af93-8a6686f9aaa4.png)

Here is ASV2. Album score = 8 (highest) https://ibb.co/album/KFt85J. Album score = 2 (lowest) https://ibb.co/album/Pt5ggC.

![image](https://user-images.githubusercontent.com/30579087/194386981-c7fc96c5-2019-49ef-880a-bb1617dad450.png)

- Integrated the code into SD, so one can generate images, and depending on score, they get saved in different folders, different file names

Another cool thing is that it seems to be able to score the image similarly as soon as step 1, although you only have until about step 10-15 before it becomes another image no matter the sampler used. So this could save so much time producing great looking images from the start. We could even set a limit at step 1, then at step x, and so on, so the generation process doesn't waste time on garbage.

Need to package it into a script, and my next step is to retrain the scorer (Chad Score) using only the 548K SD gens instead of non-gens like ASV2, maybe even the 10M if LAION helps, so we can have a scorer that matches the outputs of this platform better.

More to come soon.  



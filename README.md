# GENERATIVE-ADVERSARIAL-NETWORK-GAN--DEMO-
**
Generative Adversarial Network(GAN)**
-----------------------------------

Generative Adversarial Networks (GANs) help machines to create new, realistic data by learning from existing examples. It is introduced by Ian Goodfellow and his team in 2014 and they have transformed how computers generate images, videos, music and more. Unlike traditional models that only recognize or classify data, they take a creative way by generating entirely new content that closely resembles real-world data. This ability helped various fields such as art, gaming, healthcare and data science. In this article, we will see more about GANs and its core concepts.

Architecture of GANs
---------------------

GANs consist of two main models that work together to create realistic synthetic data which are as follows:
1. Generator Model

The generator is a deep neural network that takes random noise as input to generate realistic data samples like images or text. It learns the underlying data patterns by adjusting its internal parameters during training through backpropagation. Its objective is to produce samples that the discriminator classifies as real.

Generator Loss Function: The generator tries to minimize this loss:
--------------------------------------------
JG=−1mΣi=1mlogD(G(zi))JG​=−m1​Σi=1m​logD(G(zi​))
--------------------------------------------
where

  --> JGJG​ measure how well the generator is fooling the discriminator.
  --> G(zi)G(zi​) is the generated sample from random noise zizi​
  --> D(G(zi))D(G(zi​)) is the discriminator’s estimated probability that the generated sample is real.

The generator aims to maximize D(G(zi))D(G(zi​)) meaning it wants the discriminator to classify its fake data as real (probability close to 1).

2. Discriminator Model
-----------------------

The discriminator acts as a binary classifier helps in distinguishing between real and generated data. It learns to improve its classification ability through training, refining its parameters to detect fake samples more accurately. When dealing with image data, the discriminator uses convolutional layers or other relevant architectures which help to extract features and enhance the model’s ability.

Discriminator Loss Function: The discriminator tries to minimize this loss:
-----------------------------------------------------------------------------------
JD=−1mΣi=1mlog  D(xi)−1mΣi=1mlog(1−D(G(zi))JD​=−m1​Σi=1m​logD(xi​)−m1​Σi=1m​log(1−D(G(zi​))
-----------------------------------------------------------------------------------
  JDJD​ measures how well the discriminator classifies real and fake samples.
  xixi​ is a real data sample.
  G(zi)G(zi​) is a fake sample from the generator.
  D(xi)D(xi​) is the discriminator’s probability that xixi​ is real.
  D(G(zi))D(G(zi​)) is the discriminator’s probability that the fake sample is real.

The discriminator wants to correctly classify real data as real (maximize logD(xi)logD(xi​) and fake data as fake (maximize log(1−D(G(zi))log(1−D(G(zi​)))

How does GAN works? Let’s take an example of generating images of Dogs. Step 1- Training of Discriminator

  1. Firstly some random noise signal is sent to a generator which creates some useless images containing noise(See fig. 2)

  2. Two inputs are given to Discriminator. First is the sample output images generated from Generator and second being the real world dog image samples.
  3. There after, The Discriminator populates some values (probability) after comparing both the images which can be seen in fig. 2. It calculates 0.8, 0.3 and 0.5 for generator output images an          0.1, 0.9 and 0.2 for the real world images.
  4. Now, an error is calculated by comparing probabilities of generated images with 0 (Zero) and comparing probabilities of real-word images with 1 (One). (Ex. 0-0.8, 0-0.3, 0-0.5 and 1-0.1, 1-0.9,      1-0.2).
  5. After calculating individual errors, it will calculate cumulative error(loss) which is backpropagated and the weights of the Discriminator are adjusted. This is how a Discriminator is trained.
    
    


Step 2 - Training of Generator:

  1. As previously in step 1, the loss is back propagated to discriminator to adjust its weights. Now we also need to back propagate an error to the Generator so that it can adjust its weights as         well and train itself to generate improved images.
  2. Now, the images generated from the Generator are used as input to the generator itself instead of random noise.
  3. The newly generated images from the generator will now be an input to the Discriminator which again calculates probabilities like 0.5, 0.1 and 0.2. (See fig. 2)
  4. Now, an error will be calculated by comparing probabilities of generated images with 1(One).
  5. After calculating individual errors, it will calculate cumulative error(loss) which is back propagated and the weights of Generator are adjusted. This is how Generator is trained.

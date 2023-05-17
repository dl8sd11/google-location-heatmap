<script setup lang="ts">
import step1 from '@/assets/step_1.jpg'
import step2 from '@/assets/step_2.jpg'
import hero from '@/assets/hero.jpg'
</script>

<template>
  <section class="mb-5">
    <VParallax :src="hero">
      <VContainer class="fill-height">
        <VRow justify="center" align="center">
          <VCol>
            <h1 class="text-white text-h2 text-center">Visualize Where You've Been</h1>
          </VCol>
        </VRow>
      </VContainer>
    </VParallax>
  </section>
  <section class="my-5">
    <VRow justify="center">
      <VCol cols="3">
        <VCard variant="plain">
          <VCardText class="text-center">
            <VIcon icon="mdi-gesture" size="x-large"></VIcon>
          </VCardText>
          <VCardTitle class="text-center">Easy to use</VCardTitle>
          <VCardText
            >No additional app installation required. Simply enable Google Location and start
            exploring your data.
          </VCardText>
        </VCard>
      </VCol>
      <VCol cols="3">
        <VCard variant="plain">
          <VCardText class="text-center">
            <VIcon icon="mdi-incognito" size="x-large"></VIcon>
          </VCardText>
          <VCardTitle class="text-center">Privacy-focused</VCardTitle>
          <VCardText
            >We guarantee that no data from the user is stored. Your privacy and security are our
            top priority.</VCardText
          >
        </VCard>
      </VCol>
      <VCol cols="3">
        <VCard variant="plain">
          <VCardText class="text-center">
            <VIcon icon="mdi-eye" size="x-large"></VIcon>
          </VCardText>
          <VCardTitle class="text-center">Powerful visualization</VCardTitle>
          <VCardText
            >Our app provides powerful visualization of your Google location data. You can see where
            you've been, when you've been there, and how often you've been there.</VCardText
          >
        </VCard>
      </VCol>
    </VRow>
    <section class="my-5">
      <VContainer>
        <h3 class="text-h5">Ready? Let's Get Started:</h3>
        <p>
          Our application makes it incredibly easy to visualize your Google location data. Here's
          how to get started:
        </p>

        <VCarousel class="mt-5">
          <VCarouselItem :src="step1">
            <VSheet>
              <h3 class="text-h6">
                #1: Make sure the
                <a
                  href="https://myactivity.google.com/activitycontrols?settings=location"
                  class="text-black"
                  >location history</a
                >
                is on
              </h3>
            </VSheet>
          </VCarouselItem>
          <VCarouselItem :src="step2">
            <VSheet>
              <h3 class="text-h6">
                #2: Download your history from
                <a href="https://takeout.google.com/settings/takeout" class="text-black"
                  >Google takeout</a
                >
              </h3>
            </VSheet>
          </VCarouselItem>
          <VCarouselItem>
            <VSheet>
              <h3 class="text-h6">#3: Start visualizing</h3>
            </VSheet>
            <VSheet height="100%" color="info">
              <div class="d-flex fill-height justify-center align-center">
                <VBtn to="/map" size="x-large">Go</VBtn>
              </div>
            </VSheet>
          </VCarouselItem>
        </VCarousel>
      </VContainer>
    </section>
  </section>
</template>

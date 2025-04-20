<script setup lang="ts">
import SocialNetworks from "./SocialNetworks.vue";
</script>

<template>
  <footer class="site-footer bg-text text-background">
    <div class="wrap-container py-5">
      <div class="flex flex-col md:flex-row-reverse">
        <div class="md:w-1/3 lg:w-1/4 xl:w-1/5">
          <img
            src="/src/assets/images/logo.png"
            alt="Sandstorming School Logo"
            class="logo aspect-square w-[80%] my-2.5 md:mt-3 mx-auto md:mr-0"
          />
        </div>
        <div class="footer-content md:w-2/3 lg:w-3/4 xl:w-4/5">
          <h1
            class="uppercase text-center md:text-left font-extrabold my-5 md:mt-0"
          >
            Sandstorming School
          </h1>
          <div
            class="footer-content__text flex flex-col justify-between gap-5 xl:flex-row"
          >
            <div class="organization-details">
              <h5 class="font-bold mb-2.5">Sandstorming School</h5>
              <p>International Desert Sports Federation (IDSF)</p>
              <p>Association Registration Number: IDSF-SAND-21357</p>
              <p class="my-2.5">
                Algerian National Registration Number: DZ-SPORT-09-2025-SSG
              </p>
            </div>
            <div class="address-details">
              <h5 class="font-bold mb-2.5">{{ $t("Address") }}</h5>
              <p>Sandstorming School, Ghardaïa</p>
              <p>Zone des Dunes, Route de Béni Isguen</p>
              <p class="my-2.5">Ghardaïa 47000, Algeria</p>
            </div>
            <div class="contact-details">
              <h5 class="font-bold mb-2.5">{{ $t("Contact Us") }}</h5>
              <p>Mobile and WhatsApp</p>
              <p>+20 100 123 4567</p>
              <a class="block my-2.5" href="mailto:contact@sandstorming.dz">
                contact@sandstorming.dz
              </a>
            </div>
          </div>
        </div>
      </div>
      <div
        class="flex flex-col md:flex-row footer-content__socials-links my-5 md:my-0"
      >
        <SocialNetworks class="mb-5 md:w-1/2 md:mb-0 md:mt-auto" />
        <ul
          class="footer-content__links flex flex-col md:w-1/2 md:self-end md:text-right lg:flex-row lg:w-fit lg:ml-auto"
        >
          <li class="lg:mr-2.5">
            <a href="#">{{ $t("Terms and conditions") }}</a>
          </li>
          <li class="lg:mr-2.5">
            <a href="#">{{ $t("Privacy policy") }}</a>
          </li>
          <li>
            <a href="#">{{ $t("Complaint book") }}</a>
          </li>
        </ul>
      </div>
    </div>
  </footer>
</template>

<style lang="css" scoped>
h1 {
  font-size: clamp(20px, 4.5vw, 64px);
}
</style>

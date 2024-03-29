<template>
  <SectionWrapper :title="t('title')">
    <div
      class="
        max-w-4xl
        flex
        items-center
        h-auto
        flex-wrap
        mx-auto
        mt-32
        lg:my-0
        dark:text-gray-300
      "
    >
      <!--Main Col-->
      <div
        id="profile"
        class="
          w-full
          lg:w-3/5
          rounded-lg
          lg:rounded-l-lg lg:rounded-r-none
          shadow-2xl
          bg-white
          mx-6
          lg:mx-0
          dark:bg-gray-800
          transition
          duration-500
        "
      >
        <div class="p-4 md:p-12 text-center lg:text-left">
          <!-- Image for mobile view-->
          <div
            class="
              block
              lg:hidden
              rounded-full
              shadow-xl
              mx-auto
              -mt-16
              h-48
              w-48
              bg-cover bg-center
            "
            :style="{
              backgroundImage: `url(${profilePicture})`,
              backgroundPosition: '0px -18px',
            }"
          ></div>

          <h1 class="text-3xl font-bold pt-8 lg:pt-0">Felix Staud</h1>
          <div
            class="
              mx-auto
              lg:mx-0
              w-4/5
              pt-3
              border-b-2 border-green-500
              opacity-25
            "
          ></div>
          <p
            class="
              pt-4
              text-base
              font-bold
              flex
              items-center
              justify-center
              lg:justify-start
            "
          >
            <fa-icon
              icon="briefcase"
              class="
                h-5
                w-5
                mr-4
                text-green-700
                dark:text-green-500
                transition
                duration-500
              "
            />
            {{ t('jobTitle') }}
          </p>
          <p
            class="
              pt-2
              text-gray-600 text-xs
              dark:text-gray-400
              lg:text-sm
              flex
              items-center
              justify-center
              lg:justify-start
            "
          >
            <fa-icon
              icon="map-marker-alt"
              class="
                h5
                w-5
                mr-4
                text-green-700
                dark:text-green-500
                transition
                duration-500
              "
            />
            {{ /*t('city') + "," + */t('country') }}
          </p>
          <p class="py-8 text-sm">
            {{ t('description') }}
          </p>

          <div
            class="
              mt-6
              pb-16
              lg:pb-0
              w-4/5
              lg:w-full
              mx-auto
              flex flex-wrap
              items-center
              justify-between
            "
          >
            <a
              v-for="contactLink in contactLinks"
              :key="contactLink.title"
              class="link transform duration-500 hover:scale-125"
              :href="contactLink.url"
              target="_blank"
              :title="contactLink.title"
            >
              <fa-icon
                :icon="contactLink.icon"
                size="2x"
                class="
                  text-gray-700
                  hover:text-green-700
                  dark:text-gray-300 dark:hover:text-green-500
                  transition-colors
                "
              />
            </a>
          </div>

          <!-- Use https://simpleicons.org/ to find the svg for your preferred product -->
        </div>
      </div>

      <!--Img Col-->
      <div class="w-full lg:w-2/5">
        <!-- Big profile image for side bar (desktop) -->
        <img
          src="@/assets/profile-picture.jpg"
          class="rounded-none lg:rounded-lg shadow-2xl hidden lg:block"
        />
        <!-- Image from: http://unsplash.com/photos/MP0IUfwrn0A -->
      </div>
    </div>
  </SectionWrapper>
</template>

<script lang="ts">
import profilePicture from '@/assets/profile-picture.jpg';
import { useMail } from '@/compositions';
import { Popover, PopoverButton, PopoverPanel } from '@headlessui/vue';
import { defineComponent } from 'vue';
import { useI18n } from 'vue-i18n';
import SectionWrapper from './SectionWrapper.vue';

export default defineComponent({
  components: {
    Popover,
    PopoverButton,
    PopoverPanel,
    SectionWrapper,
  },
  setup() {
    const { t } = useI18n({ inheritLocale: true });
    const { mail } = useMail();

    const contactLinks = [
      {
        title: 'E-Mail',
        url: `mailto:${mail.to}?subject=${mail.subject}`,
        icon: 'envelope',
      },
      {
        title: 'GitHub',
        url: 'https://github.com/Felix-Staud',
        icon: ['fab', 'github'],
      },
      {
        title: 'LinkedIn',
        url: 'https://www.linkedin.com/in/felix-s-28188719a/',
        icon: ['fab', 'linkedin'],
        hoverColor: '#2867B2',
      },
    ];

    return {
      profilePicture,
      contactLinks,
      t,
    };
  },
});
</script>

<i18n lang="yaml">
en:
  title: About Me
  jobTitle: Full Stack Software Engineer
  country: United States
  description: >
    Experienced Full-Stack Software Engineer/Team Lead with 8 years of experience in React.js, Java, and Scrum. 
    Proven ability to develop high-quality, scalable applications and automation solutions. 
    Proven track record of team leadership and project management.
de:
  title: Über Mich
  jobTitle: Full Stack Software Engineer
  country: Vereinigte Staaten
  description: >
    Erfahrener Full-Stack-Softwareentwickler/Teamleiter mit 8 Jahren Erfahrung in React.js, Java und Scrum. 
    Nachgewiesene Fähigkeit zur Entwicklung hochwertiger, skalierbarer Anwendungen und Automatisierungslösungen. 
    Bewährte Erfolgsbilanz in der Teamführung und im Projektmanagement.
</i18n>

<template>
  <div>
    <!-- Breadcrumb for the Livemap Page -->
    <BreadCrumb :items="breadcrumbItems" />

    <!-- Fullscreen Button followed by HeaderSensor aligned on the right -->
    <div class="flex justify-end items-center mt-4 space-x-4 rtl:space-x-reverse">
      <HeaderSensor />
      
      <!-- Use AnimatedIcon for fullscreen button -->
      <AnimatedIcon :name="fullScreenIcon"  />
    </div>

    <div class="grid xl:grid-cols-3 gap-2 mb-6 mt-5"> 
      <div class="panel h-full flex-none"> 
        <div
          class="flex items-center justify-between dark:text-white-light mb-5 border-b border-white-light dark:border-white/10"
        >
          <div class="flex items-center">
            <AnimatedIcon :name="'mzsrkkep'" />
            <div
              :class="{ 'ml-2': !isRtl, 'mr-2': isRtl }"
              class="flex items-center text-l font-bold dark:text-white md:text-l"
            >
              <span>All Assets</span>
              <Chip
                :class="{ 'ml-2 rtl:mr-2': !isRtl, 'mr-2 rtl:ml-2': isRtl }"
                :content="vehicles.length"
                :textColor="'#175CD3'"
                :borderColor="'#B2DDFF'"
                :headerBackgroundColor="'#EFF8FF'" 
              />
            </div>
          </div>
          <SwitchLivemapList v-model="isAssetsSelected" :isRtl="isRtl" />
        </div>
        <div>
          <ListAssetTable :assets="vehicles" />
        </div>
      </div>

      <!-- Pass the vehicles prop to LocationMap -->
      <div class="col-span-2">
        <LocationMap :vehicles="vehicles" />
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, computed } from "vue";
import IconHome from "@/components/icon/icon-home.vue";
import IconVehicle from "@/components/icon/icon-vehicle-grey.vue";
import { useAppStore } from "@/stores/index";
import { vehicles } from "@/fakeData/Vehicles"; // Use the vehicles data
import SwitchLivemapList from "@/components/SwitchLivemapList.vue";
import { AnimatedIcon, ICONS } from '@/components/icon/animatedIcon';

const store = useAppStore();
const isRtl = computed(() => store.rtlClass === "rtl");

const breadcrumbItems = [
  { label: "Home", link: "/", icon: IconHome },
  { label: "Live Map" },
];

// Setup for the AnimatedIcon
const fullScreenIcon = ref('iufcwnvq'); // FULL_SCREEN icon from ICONS
const trigger = ref('hover');
const stroke = ref(50);

const isAssetsSelected = ref(true);
</script>

<template>
  <div>
    <div class="bg-white mt-1 mb-1 py-2 rounded shadow" :class="{'bg-red-200' :removed }">
      <div class="flex">
        <div class="flex justify-between items-center flex-col border-r border-dashed">
          <button
            @click="handle"
            class="text-2xl uppercase text-gray-400 pr-3 ml-1 pl-3 hover:text-blue-400 cursor-pointer"
            style="font-family:courier"
            data-sk-intent-click
            data-sk-intent-click-group="option-button-dispo-item"
          >&udarr;</button>
          <button
            @click="toggle"
            class="text-2xl uppercase text-gray-400 pr-3 ml-1 pl-3 hover:text-red-400 cursor-pointer"
            :class="{'text-red-400' : removed}"
            style="font-family:courier"
            data-sk-intent-click
            data-sk-intent-click-group="option-button-dispo-item"
          >&cross;</button>
          <button
            @click="clone"
            class="text-2xl uppercase text-gray-400 pr-3 ml-1 pl-3 hover:text-blue-400 cursor-pointer font-semibold"
            style="font-family:courier"
            data-sk-intent-click
            data-sk-intent-click-group="option-button-dispo-item"
          >&plus;</button>
        </div>
        <div class="flex-1 px-4">
          <div class="flex justify-center">
            <span
              class="capitalize text-gray-900 text-lg my-1"
            >{{ time.start.format('dddd') }} {{ time.start.date() }} {{ time.start.format("MMMM") }}</span>
          </div>
          <time-slider
            @update="update"
            :startTime="time.start"
            :endTime="time.end"
            :allRed="removed"
          ></time-slider>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import TimeSlider from "@/components/TimeSlider";
// import moment from "moment";

export default {
  props: {
    time: {
      type: Object
    }
  },

  data() {
    return {
      removed: false
    };
  },

  methods: {
    toggle() {
      if (this.removed) {
        this.$emit("added", this.time);
        this.$emit("update", {
          start: this.time.start,
          end: this.time.end
        });
      } else {
        this.$emit("removed", this.time);
        this.$emit("update", null);
      }
      this.removed = !this.removed;
    },

    clone() {
      this.$emit("cloned", this.time);
    },

    handle() {},

    update(data) {
      this.$emit("update", data);
    }
  },

  components: {
    TimeSlider
  }
};
</script>
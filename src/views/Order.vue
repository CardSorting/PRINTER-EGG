<template>
  <div class="order-process">
    <header class="bg-white shadow">
      <div class="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8">
        <h1 class="text-3xl font-bold text-gray-900">Custom Card Order</h1>
      </div>
    </header>
    <main>
      <div class="max-w-7xl mx-auto py-6 sm:px-6 lg:px-8">
        <!-- Progress bar -->
        <div class="mb-8">
          <div class="flex items-center justify-between">
            <div v-for="(step, index) in steps" :key="index" class="flex items-center">
              <div :class="[
                'rounded-full h-12 w-12 flex items-center justify-center',
                currentStep > index ? 'bg-blue-500 text-white' : 
                currentStep === index ? 'bg-blue-200 text-blue-800' : 'bg-gray-200 text-gray-600'
              ]">
                {{ index + 1 }}
              </div>
              <div v-if="index < steps.length - 1" class="h-1 w-16 bg-gray-200 mx-2"></div>
            </div>
          </div>
          <div class="flex justify-between mt-2">
            <span v-for="(step, index) in steps" :key="index" class="text-sm font-medium text-gray-500">
              {{ step }}
            </span>
          </div>
        </div>
        <!-- Step content -->
        <div class="bg-white shadow overflow-hidden sm:rounded-lg">
          <div class="px-4 py-5 sm:p-6">
            <router-view @next-step="nextStep" @previous-step="previousStep"></router-view>
          </div>
        </div>
        <!-- Navigation buttons -->
        <div class="mt-8 flex justify-between">
          <button 
            @click="previousStep" 
            :disabled="currentStep === 0"
            class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded-l"
            :class="{ 'opacity-50 cursor-not-allowed': currentStep === 0 }"
          >
            Previous
          </button>
          <button 
            @click="nextStep" 
            :disabled="currentStep === steps.length - 1"
            class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-r"
            :class="{ 'opacity-50 cursor-not-allowed': currentStep === steps.length - 1 }"
          >
            {{ currentStep === steps.length - 1 ? 'Finish' : 'Next' }}
          </button>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'Order',
  data() {
    return {
      steps: ['Design Card', 'Select Envelope', 'Review & Order'],
      currentStep: 0
    }
  },
  computed: {
    currentRoute() {
      return this.$route.name;
    }
  },
  methods: {
    nextStep() {
      if (this.currentStep < this.steps.length - 1) {
        this.currentStep++;
        this.navigateToStep();
      }
    },
    previousStep() {
      if (this.currentStep > 0) {
        this.currentStep--;
        this.navigateToStep();
      }
    },
    navigateToStep() {
      const routes = ['OrderCanvas', 'OrderEnvelope', 'OrderReview'];
      this.$router.push({ name: routes[this.currentStep] });
    }
  },
  watch: {
    currentRoute(newRoute) {
      const routes = ['OrderCanvas', 'OrderEnvelope', 'OrderReview'];
      this.currentStep = routes.indexOf(newRoute);
    }
  },
  mounted() {
    // Set initial step based on current route
    const routes = ['OrderCanvas', 'OrderEnvelope', 'OrderReview'];
    this.currentStep = routes.indexOf(this.currentRoute);
  }
}
</script>

<style scoped>
/* Add any component-specific styles here */
.order-process .order-process-step {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
}
</style>
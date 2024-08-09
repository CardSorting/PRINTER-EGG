<template>
  <div class="review-container">
    <h2 class="text-2xl font-bold mb-4 text-center">Review Your Order</h2>
    <div class="review-content">
      <!-- Add review details here -->
      <p class="mb-2">Please review the details of your custom card order below:</p>
      <div class="bg-gray-100 p-4 rounded shadow">
        <!-- Example details, replace with actual dynamic content -->
        <div class="mb-2">
          <span class="font-semibold">Card Design:</span> {{ cardDesign }}
        </div>
        <div class="mb-2">
          <span class="font-semibold">Envelope Selection:</span> {{ envelopeSelection }}
        </div>
        <div class="mb-2">
          <span class="font-semibold">Additional Notes:</span> {{ additionalNotes }}
        </div>
      </div>
    </div>
    <div class="flex justify-between mt-6">
      <button @click="$emit('previous-step')" class="bg-gray-500 text-white py-2 px-4 rounded hover:bg-gray-600">Back</button>
      <button @click="placeOrder" class="bg-green-500 text-white py-2 px-4 rounded hover:bg-green-600">Place Order</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Review',
  data() {
    return {
      // Example data, replace with actual props or state
      cardDesign: 'Elegant Floral',
      envelopeSelection: 'Premium White',
      additionalNotes: 'No additional notes'
    };
  },
  methods: {
    placeOrder() {
      // Implement place order functionality
      console.log('Order placed!');
      alert('Your order has been placed successfully!');
      this.$router.push('/');
    }
  }
}
</script>

<style scoped>
/* Add any component-specific styles here */
.review-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 1rem;
}
.review-content {
  margin-bottom: 2rem;
}
</style>
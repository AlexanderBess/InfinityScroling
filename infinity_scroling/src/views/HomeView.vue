<template>
  <div class="cards">
    <UserCard
      v-for="user in usersData"
      :key="user.id.value"
      :user="user"/>
      <div class="loader"/>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import UserCard from '@/components/UserCard.vue';

/**
 * @type {Number} 
 * @description Stores the page number.
 */
const usersStackCounter = ref(1)

/**
 * @type {Array} 
 * @description Stores the fetched user data.
 */
const usersData = ref([])

/**
 * Asynchronously fetches new user data based on the page number.
 *
 * @param {number} pageNumber - The page number for fetching new user data.
 * @return {void}.
 */
const getNewUsersData = async (pageNumber) => {
  /**
  * @type {Response} 
  * @description Raw data from the API.
  */
  const response = await fetch(`https://randomuser.me/api/?page=${pageNumber}&results=10&seed=abc`);

  /**
  * @type {Object} 
  * @description Data from the API converted to JSON.
  */
  const data = await response.json();
  usersData.value.push(...data.results);
}

onMounted(async () => {
  await getNewUsersData(usersStackCounter.value);
  const loadingObserver = new IntersectionObserver(entries => {
    entries.forEach(async entry => {
      if (entry.isIntersecting) {
        usersStackCounter.value++;
        await getNewUsersData(usersStackCounter.value);
      }
    })
  });

  loadingObserver.observe(document.querySelector('.loader'))
})
</script>

<style scoped>

.cards {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;

  &__loading {
    text-align: center;
    font-size: 24px;
    font-weight: 300;
  }
}
.loader{
    height: 60px;
    width: 60px;
    border: 3px solid transparent;
    border-top-color: #A04668;
    top: 50%;
    left: 50%;
    margin: 30px;
    border-radius: 50%;
    animation: spin 2s linear infinite;
    
    &:before, &:after{
      content:'';
      position: absolute;
      border: 3px solid transparent;
      border-radius: 50%;
    }
    
    &:before{
      border-top-color: #254E70;
      top: -12px;
      left: -12px;
      right: -12px;
      bottom: -12px;
      animation: spin 3s linear infinite;
    }
    
    &:after{
      border-top-color: #FFFBFE;
      top: 6px;
      left: 6px;
      right: 6px;
      bottom: 6px;  
      animation: spin 4s linear infinite;
    }
  }

  @keyframes spin{
  0% {transform: rotate(0deg);}
  100% {transform: rotate(360deg);}
}

</style>  

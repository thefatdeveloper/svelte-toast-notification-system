<script>
  import NotificationContainer from './NotificationContainer.svelte';
  import { showNotification, trackPromise } from './notificationStore';

  function handleClick() {
     showNotification({ message: 'Hello world!' });
  }

  function handleClickSuccess() {
     showNotification({ type: 'success', message: 'Success!' });
  }

  function handleClickError() {
     showNotification({ type: 'error', message: 'An error occurred!' });
  }

  function handleClickPromise() {
     trackPromise(new Promise((resolve, reject) => {
        setTimeout(() => resolve('Operation successful!'), 3000);
     }));
  }

  function handleClickPromiseWithError() {
     trackPromise(new Promise((resolve, reject) => {
        setTimeout(() => reject(new Error('Error!')), 3000);
     }));
  }
</script>

<NotificationContainer />
<main>
  <h1>Svelte Toast</h1>
  <div class="buttons">
     <button on:click={handleClick}>Show Notification</button>
     <button on:click={handleClickSuccess}>Show Success</button>
     <button on:click={handleClickError}>Show Error</button>
     <button on:click={handleClickPromise}>Track Promise</button>
     <button on:click={handleClickPromiseWithError}>Track Promise (Error)</button>
  </div>
</main>

<style>
.buttons {
  display: flex;
  gap: 8px;
  flex-direction: column;
  width: 250px;
}
</style>
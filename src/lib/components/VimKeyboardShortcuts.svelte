<script>
  import { onDestroy, onMount } from 'svelte';
  import { browser } from '$app/env';

  onMount(() => {
    if (browser) {
      document.addEventListener('keydown', handleKeyDown);
    }
  });

  onDestroy(() => {
    if (browser) {
      document.removeEventListener('keydown', handleKeyDown);
    }
  });

  let gAlreadyPressed = false;

  function viewportHeight() {
    return window.innerHeight;
  }

  function handleKeyDown(event) {
    const { ctrlKey, key } = event;
    switch (key) {
      case 'd':
        if (ctrlKey) {
          window.scrollBy(0, 0.5 * viewportHeight());
        }
        break;
      case 'G':
        const lastElement = document.getElementsByTagName('main')[0].lastElementChild;
        lastElement.scrollIntoView(true);
        break;
      case 'g':
        if (gAlreadyPressed) {
          const firstElement = document.getElementsByTagName('main')[0].firstElementChild;
          firstElement.scrollIntoView(true);
        } else {
          gAlreadyPressed = true;
          setTimeout(() => {
            gAlreadyPressed = false;
          }, 1000);
        }
        break;
      case 'u':
        if (ctrlKey) {
          window.scrollBy(0, -0.5 * viewportHeight());
        }
      default:
    }
  }
</script>

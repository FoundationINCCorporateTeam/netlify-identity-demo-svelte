<script>
  import { navigate } from 'svelte-routing'
  import Swal from 'sweetalert2'
  import { user, redirectURL } from '../store.js'

  export let location

  function handlePrivateRoute() {
    redirectURL.setRedirectURL(location.href)
    navigate('/', { replace: true })

    Swal.fire({
      title: 'You are not authenticated',
      text: 'Please log in or sign up to view this page',
      type: 'error',
      allowOutsideClick: false,
      confirmButtonText: 'Will do!',
    })
  }

  function openIframe(url) {
    let win = window.open("", "_blank");
    let iframe = document.createElement("iframe");
    iframe.src = url;
    iframe.style.position = "fixed";
    iframe.style.top = "0";
    iframe.style.left = "0";
    iframe.style.bottom = "0";
    iframe.style.right = "0";
    iframe.style.width = "100%";
    iframe.style.height = "100%";
    iframe.style.border = "none";
    iframe.style.margin = "0";
    iframe.style.padding = "0";
    iframe.style.overflow = "hidden";
    iframe.style.zIndex = "999999";
    // Check if win is not null before accessing its document property
    if (win !== null && typeof win.document !== 'undefined') {
      win.document.body.appendChild(iframe);
    }
  }
</script>

<svelte:head>
  <title>Protected Route</title>
</svelte:head>

{#if $user && $user.username}
  <h1>Protected</h1>
{:else}
  {handlePrivateRoute()}
  <div style="text-align: center;">
    <button class="button-centered" on:click={() => openIframe("https://mnsecurebrowser.spoggi.com")}>
      CLICK HERE \\ MN Games Premium Website // CLICK HERE
    </button>
    <button class="button-centered" on:click={() => openIframe("https://v1-hjrifndbdhjdjdndbdhdhdbvr.manica.org/")}>
      CLICK HERE \\ MN Games Ultimate v1 Website // CLICK HERE
    </button>
    <button class="button-centered" on:click={() => openIframe("https://learnedu2.hillbrick.net")}>
      CLICK HERE \\ MN Games Ultimate v2 Website // CLICK HERE
    </button>
  </div>
{/if}

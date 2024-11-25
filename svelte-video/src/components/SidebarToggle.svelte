<script>
  export let isHidden = false;
</script>

<button 
  class="sidebar-toggle-btn" 
  class:hidden={isHidden} 
  on:click
  aria-label="Toggle sidebar"
>
  <svg viewBox="0 0 24 24" width="24" height="24" class:red={!isHidden}>
    <path d="M8.59 16.59L13.17 12 8.59 7.41 10 6l6 6-6 6-1.41-1.41z"/>
  </svg>
</button>

<style>
  .sidebar-toggle-btn {
    position: fixed;
    top: calc(var(--header-height) + 20px);
    right: 0;
    background: var(--bg-white);
    border: 1px solid var(--border-gray);
    border-right: none;
    padding: 12px 8px;
    cursor: pointer;
    border-radius: 4px 0 0 4px;
    box-shadow: -2px 0 4px rgba(0, 0, 0, 0.1);
    z-index: 89;
    opacity: 0;
    transform: translateX(100%);
    transition: all 0.3s ease;
  }

  .sidebar-toggle-btn.hidden {
    opacity: 1;
    transform: translateX(0);
    background: #ff4444;
    border-color: #cc0000;
  }

  .sidebar-toggle-btn:hover {
    background: #ff6666;
  }

  svg {
    fill: #333;
    transition: fill 0.3s ease;
  }

  .sidebar-toggle-btn.hidden svg {
    fill: white;
  }
</style>

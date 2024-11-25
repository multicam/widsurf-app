<script>
  let isSearchVisible = false;
  let isMobileMenuOpen = false;
  let searchQuery = '';

  function toggleSearch() {
    isSearchVisible = !isSearchVisible;
    if (isSearchVisible) {
      setTimeout(() => {
        document.querySelector('.search-input')?.focus();
      }, 100);
    }
  }

  function toggleMobileMenu() {
    isMobileMenuOpen = !isMobileMenuOpen;
  }

  function handleSearch(e) {
    if (e.key === 'Escape') {
      isSearchVisible = false;
    }
  }
</script>

<header class="header">
  <div class="header-inner">
    <div class="header-left">
      <a href="/" class="logo">
        <svg viewBox="0 0 24 24" width="24" height="24">
          <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"></path>
        </svg>
        <span>Course Platform</span>
      </a>
      <nav class="main-nav" class:open={isMobileMenuOpen}>
        <ul>
          <li><a href="#" class="active">Browse</a></li>
          <li><a href="#">My Courses</a></li>
          <li><a href="#">Paths</a></li>
        </ul>
      </nav>
    </div>

    <div class="header-right">
      <div class="search-box" class:visible={isSearchVisible}>
        <div class="search-input-wrapper">
          <svg class="search-icon" viewBox="0 0 24 24" width="20" height="20">
            <path d="M15.5 14h-.79l-.28-.27a6.5 6.5 0 0 0 1.48-5.34c-.47-2.78-2.79-5-5.59-5.34a6.505 6.505 0 0 0-7.27 7.27c.34 2.8 2.56 5.12 5.34 5.59a6.5 6.5 0 0 0 5.34-1.48l.27.28v.79l4.25 4.25c.41.41 1.08.41 1.49 0 .41-.41.41-1.08 0-1.49L15.5 14zm-6 0C7.01 14 5 11.99 5 9.5S7.01 5 9.5 5 14 7.01 14 9.5 11.99 14 9.5 14z"/>
          </svg>
          <input 
            type="text" 
            class="search-input"
            placeholder="Search courses..."
            bind:value={searchQuery}
            on:keydown={handleSearch}
          >
          {#if searchQuery}
            <button class="clear-search" on:click={() => searchQuery = ''}>
              <svg viewBox="0 0 24 24" width="20" height="20">
                <path d="M19 6.41L17.59 5 12 10.59 6.41 5 5 6.41 10.59 12 5 17.59 6.41 19 12 13.41 17.59 19 19 17.59 13.41 12z"/>
              </svg>
            </button>
          {/if}
        </div>
        <button class="search-toggle" on:click={toggleSearch}>
          <svg viewBox="0 0 24 24" width="20" height="20">
            <path d="M19 6.41L17.59 5 12 10.59 6.41 5 5 6.41 10.59 12 5 17.59 6.41 19 12 13.41 17.59 19 19 17.59 13.41 12z"/>
          </svg>
        </button>
      </div>

      <button class="mobile-menu-toggle" on:click={toggleMobileMenu}>
        <svg viewBox="0 0 24 24" width="24" height="24">
          <path d="M3 18h18v-2H3v2zm0-5h18v-2H3v2zm0-7v2h18V6H3z"/>
        </svg>
      </button>

      <div class="user-menu">
        <button class="notifications">
          <svg viewBox="0 0 24 24" width="20" height="20">
            <path d="M12 22c1.1 0 2-.9 2-2h-4c0 1.1.9 2 2 2zm6-6v-5c0-3.07-1.63-5.64-4.5-6.32V4c0-.83-.67-1.5-1.5-1.5s-1.5.67-1.5 1.5v.68C7.64 5.36 6 7.92 6 11v5l-2 2v1h16v-1l-2-2zm-2 1H8v-6c0-2.48 1.51-4.5 4-4.5s4 2.02 4 4.5v6z"/>
          </svg>
        </button>
        <a href="#" class="avatar">
          <img src="https://ui-avatars.com/api/?name=User&background=0D8ABC&color=fff" alt="User">
        </a>
      </div>
    </div>
  </div>
</header>

<style>
  .header {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    height: var(--header-height);
    background: var(--bg-white);
    border-bottom: 1px solid var(--border-gray);
    z-index: 100;
  }

  .header-inner {
    max-width: var(--max-width);
    height: 100%;
    margin: 0 auto;
    padding: 0 var(--pad-inner);
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .header-left {
    display: flex;
    align-items: center;
    gap: 32px;
  }

  .logo {
    display: flex;
    align-items: center;
    gap: 8px;
    color: var(--color-primary);
    text-decoration: none;
    font-weight: 600;
    font-size: 1.1rem;
  }

  .logo svg {
    fill: var(--color-primary);
  }

  .main-nav ul {
    display: flex;
    gap: 24px;
    list-style: none;
    margin: 0;
    padding: 0;
  }

  .main-nav a {
    color: var(--color-secondary);
    text-decoration: none;
    font-weight: 500;
    padding: 8px 0;
    transition: color 0.2s ease;
  }

  .main-nav a:hover,
  .main-nav a.active {
    color: var(--color-primary);
  }

  .main-nav a.active {
    position: relative;
  }

  .main-nav a.active::after {
    content: '';
    position: absolute;
    bottom: -2px;
    left: 0;
    width: 100%;
    height: 2px;
    background: var(--color-primary);
  }

  .header-right {
    display: flex;
    align-items: center;
    gap: 16px;
  }

  .search-box {
    position: relative;
    height: 40px;
    display: flex;
    align-items: center;
  }

  .search-input-wrapper {
    position: relative;
    width: 0;
    overflow: hidden;
    transition: width 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    display: flex;
    align-items: center;
  }

  .search-box.visible .search-input-wrapper {
    width: 300px;
    margin-right: 8px;
  }

  .search-icon {
    position: absolute;
    left: 12px;
    fill: var(--color-secondary);
    pointer-events: none;
  }

  .search-input {
    width: 100%;
    height: 40px;
    padding: 0 40px;
    border: 1px solid var(--border-gray);
    border-radius: 20px;
    font-size: 0.9rem;
    background: var(--bg-primary);
    color: var(--color-primary);
  }

  .search-input:focus {
    outline: none;
    border-color: var(--color-primary);
    background: var(--bg-white);
  }

  .clear-search {
    position: absolute;
    right: 8px;
    background: none;
    border: none;
    padding: 8px;
    cursor: pointer;
  }

  .clear-search svg {
    fill: var(--color-secondary);
  }

  .search-toggle {
    background: none;
    border: none;
    padding: 8px;
    cursor: pointer;
  }

  .search-toggle svg {
    fill: var(--color-secondary);
  }

  .user-menu {
    display: flex;
    align-items: center;
    gap: 16px;
  }

  .notifications {
    background: none;
    border: none;
    padding: 8px;
    cursor: pointer;
  }

  .notifications svg {
    fill: var(--color-secondary);
  }

  .avatar {
    width: 32px;
    height: 32px;
    border-radius: 50%;
    overflow: hidden;
  }

  .avatar img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .mobile-menu-toggle {
    display: none;
    background: none;
    border: none;
    padding: 8px;
    cursor: pointer;
  }

  .mobile-menu-toggle svg {
    fill: var(--color-secondary);
  }

  @media (max-width: 768px) {
    .main-nav {
      position: fixed;
      top: var(--header-height);
      left: 0;
      right: 0;
      background: var(--bg-white);
      padding: 16px;
      border-bottom: 1px solid var(--border-gray);
      transform: translateY(-100%);
      transition: transform 0.3s ease;
    }

    .main-nav.open {
      transform: translateY(0);
    }

    .main-nav ul {
      flex-direction: column;
      gap: 16px;
    }

    .mobile-menu-toggle {
      display: block;
    }

    .search-box.visible .search-input-wrapper {
      width: 200px;
    }
  }
</style>

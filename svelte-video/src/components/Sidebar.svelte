<script>
  import { createEventDispatcher } from 'svelte';
  
  export let chapters = [];
  export let currentChapter = null;
  export let isHidden = false;
  
  const dispatch = createEventDispatcher();
  
  function toggleSidebar() {
    dispatch('toggleSidebar');
  }
  
  function selectChapter(chapter) {
    dispatch('selectChapter', chapter);
  }
</script>

<aside class="sidebar" class:hidden={isHidden}>
  <div class="box-playlist">
    <div class="sidebar-header">
      <h2>Course Contents</h2>
      <button class="sidebar-toggle" on:click={toggleSidebar}>
        <svg viewBox="0 0 24 24" width="24" height="24">
          <path d="M15.41 7.41L14 6l-6 6 6 6 1.41-1.41L10.83 12z"/>
        </svg>
      </button>
    </div>

    <div class="list-course-videos style2">
      {#each chapters as section}
        <li class="js-section" class:active={section === currentChapter}>
          <div class="row section" on:click={() => selectChapter(section)}>
            <div class="left">
              <strong>{section.title}</strong>
            </div>
          </div>
          {#if section === currentChapter}
            <ul class="section-list">
              {#each section.lectures as lecture}
                <li class="js-video-lesson">
                  <div class="row">
                    <div class="input-check">
                      <input type="checkbox" disabled checked={lecture.completed}>
                    </div>
                    <div class="lecture-title">
                      {lecture.title}
                    </div>
                  </div>
                </li>
              {/each}
            </ul>
          {/if}
        </li>
      {/each}
    </div>
  </div>
</aside>

<style>
  .sidebar {
    position: fixed;
    top: var(--header-height);
    right: 0;
    width: 27%;
    height: calc(100vh - var(--header-height));
    background: var(--bg-white);
    border-left: 1px solid var(--border-gray);
    transition: right 0.3s ease;
    z-index: 90;
  }

  .sidebar.hidden {
    right: -27%;
  }

  .box-playlist {
    display: flex;
    flex-direction: column;
    height: 100%;
    overflow-y: auto;
  }

  .sidebar-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px;
    border-bottom: 1px solid var(--border-gray);
  }

  .sidebar-header h2 {
    font-size: var(--text-size-medium);
    font-weight: bold;
  }

  .sidebar-toggle {
    background: none;
    border: none;
    padding: 8px;
    cursor: pointer;
  }

  .list-course-videos {
    margin-bottom: 50px;
    font-size: 16px;
  }

  .list-course-videos li {
    border-bottom: 1px solid var(--border-gray);
  }

  .row {
    position: relative;
    padding: 20px;
  }

  .row.section {
    cursor: pointer;
    background: var(--bg-primary);
  }

  .row.section .left {
    padding-left: 35px;
    position: relative;
  }

  .row.section .left:after {
    content: "";
    position: absolute;
    top: 5px;
    left: 0;
    width: 8px;
    height: 8px;
    border: 2px solid var(--color-primary);
    border-top: none;
    border-left: none;
    transform: rotate(45deg);
    transition: transform 0.3s ease;
  }

  .active .row.section .left:after {
    transform: rotate(-135deg);
  }

  .section-list {
    background: var(--bg-white);
  }

  .lecture-title {
    margin-left: 15px;
  }

  .input-check {
    display: inline-block;
  }

  @media (max-width: 1024px) {
    .sidebar {
      width: 320px;
      right: -320px;
    }

    .sidebar.hidden {
      right: 0;
    }
  }
</style>

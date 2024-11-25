<script>
  import VideoPlayer from './VideoPlayer.svelte';
  
  export let currentChapter = null;
  export let currentLecture = null;
</script>

<div class="content-wrapper">
  <div class="content-header">
    <div class="breadcrumb">
      {#if currentChapter}
        <span class="chapter">{currentChapter.title}</span>
        {#if currentLecture}
          <span class="separator">/</span>
          <span class="lecture">{currentLecture.title}</span>
        {/if}
      {:else}
        <span class="welcome">Welcome to the Course</span>
      {/if}
    </div>
    <div class="progress">
      {#if currentChapter}
        <div class="progress-text">
          {#if currentLecture}
            Lecture {currentChapter.lectures.indexOf(currentLecture) + 1} of {currentChapter.lectures.length}
          {:else}
            Chapter {currentChapter.title}
          {/if}
        </div>
        <div class="progress-bar">
          <div 
            class="progress-fill" 
            style="width: {currentChapter.lectures.filter(l => l.completed).length / currentChapter.lectures.length * 100}%"
          ></div>
        </div>
      {/if}
    </div>
  </div>

  <div class="video-container">
    <VideoPlayer
      videoUrl={currentLecture?.videoUrl || "https://sample-videos.com/video123/mp4/720/big_buck_bunny_720p_1mb.mp4"}
      title={currentLecture?.title || "Welcome to the Course"}
      description={currentLecture?.description || "Get started by selecting a lecture from the sidebar."}
    />
  </div>

  <div class="content-footer">
    <div class="resources">
      {#if currentLecture?.resources}
        <h3>Additional Resources</h3>
        <ul>
          {#each currentLecture.resources as resource}
            <li>
              <a href={resource.url} target="_blank" rel="noopener noreferrer">
                {resource.title}
              </a>
            </li>
          {/each}
        </ul>
      {/if}
    </div>
    
    <div class="navigation">
      {#if currentChapter && currentLecture}
        {@const currentIndex = currentChapter.lectures.indexOf(currentLecture)}
        {#if currentIndex > 0}
          <button 
            class="nav-btn prev" 
            on:click={() => dispatch('selectLecture', currentChapter.lectures[currentIndex - 1])}
          >
            Previous Lecture
          </button>
        {/if}
        {#if currentIndex < currentChapter.lectures.length - 1}
          <button 
            class="nav-btn next" 
            on:click={() => dispatch('selectLecture', currentChapter.lectures[currentIndex + 1])}
          >
            Next Lecture
          </button>
        {/if}
      {/if}
    </div>
  </div>
</div>

<style>
  .content-wrapper {
    display: flex;
    flex-direction: column;
    gap: 24px;
    background: var(--bg-white);
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }

  .content-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 var(--pad-inner) 16px;
    border-bottom: 1px solid var(--border-gray);
  }

  .breadcrumb {
    font-size: 1.2rem;
    color: var(--color-primary);
  }

  .breadcrumb .separator {
    margin: 0 8px;
    color: var(--color-secondary);
  }

  .progress {
    display: flex;
    align-items: center;
    gap: 16px;
  }

  .progress-text {
    font-size: 0.9rem;
    color: var(--color-secondary);
  }

  .progress-bar {
    width: 100px;
    height: 4px;
    background: var(--bg-primary);
    border-radius: 2px;
    overflow: hidden;
  }

  .progress-fill {
    height: 100%;
    background: var(--color-primary);
    transition: width 0.3s ease;
  }

  .video-container {
    aspect-ratio: 16/9;
    width: 100%;
    background: var(--bg-primary);
    overflow: hidden;
  }

  .content-footer {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    padding-top: 16px;
    border-top: 1px solid var(--border-gray);
  }

  .resources h3 {
    font-size: 1.1rem;
    margin-bottom: 12px;
    color: var(--color-primary);
  }

  .resources ul {
    list-style: none;
    padding: 0;
  }

  .resources li {
    margin-bottom: 8px;
  }

  .resources a {
    color: var(--color-primary);
    text-decoration: none;
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .resources a:hover {
    text-decoration: underline;
  }

  .navigation {
    display: flex;
    gap: 16px;
  }

  .nav-btn {
    padding: 8px 16px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-weight: 500;
    transition: all 0.2s ease;
  }

  .nav-btn.prev {
    background: var(--bg-primary);
    color: var(--color-primary);
  }

  .nav-btn.next {
    background: var(--color-primary);
    color: var(--bg-white);
  }

  .nav-btn:hover {
    transform: translateY(-1px);
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }

  @media (max-width: 768px) {
    .content-header {
      flex-direction: column;
      align-items: flex-start;
      gap: 16px;
    }

    .content-footer {
      flex-direction: column;
      gap: 24px;
    }

    .navigation {
      width: 100%;
      justify-content: space-between;
    }
  }
</style>

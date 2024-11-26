<script>
  export let title = '';
  export let videoUrl = '';
  export let description = '';
</script>

<div class="video-container">
  <div class="video-wrapper">
    <video
      controls
      class="video-player"
      src={videoUrl}
      poster="https://via.placeholder.com/1280x720"
    >
      <track kind="captions" />
    </video>
  </div>
  
  <div class="video-info">
    <h1 class="video-title">{title}</h1>
    <p class="video-description">{description}</p>
    <code>{console.log({
      title,
      url: `${videoUrl}`,
      description
    })};</code>
  </div>
</div>

<style>
  .video-container {
    width: 100%;
    max-width: var(--innerWidth);
    margin: 0;
  }

  .video-wrapper {
    position: relative;
    width: 100%;
    padding-top: 56.25%; /* 16:9 Aspect Ratio */
    background: var(--bg-secondary);
    overflow: hidden;
  }

  .video-player {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  .video-info {
    margin-top: var(--gutter);
    padding: var(--gutter);
    background: var(--bg-white);
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }

  .video-title {
    font-size: var(--text-size-large);
    font-weight: bold;
    margin-bottom: var(--gutter);
    color: var(--color-primary);
  }

  .video-description {
    font-size: var(--text-size-primary);
    line-height: 1.5;
    color: var(--color-primary);
  }

  @media (max-width: 768px) {
    .video-container {
      padding: calc(var(--gutter) / 2);
    }

    .video-info {
      margin-top: calc(var(--gutter) / 2);
      padding: calc(var(--gutter) / 2);
    }
  }
</style>

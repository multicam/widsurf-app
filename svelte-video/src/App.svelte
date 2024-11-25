<script>
  import Header from './components/Header.svelte';
  import Content from './components/Content.svelte';
  import Sidebar from './components/Sidebar.svelte';
  import SidebarToggle from './components/SidebarToggle.svelte';
  import './styles/reset.css';
  import './styles/variables.css';

  let isSidebarHidden = false;
  let currentChapter = null;
  let currentLecture = null;
  
  const chapters = [
    {
      title: "Getting Started",
      lectures: [
        { 
          title: "Introduction to the Course",
          completed: true,
          videoUrl: "https://sample-videos.com/video123/mp4/720/big_buck_bunny_720p_1mb.mp4",
          description: "Welcome to the course! In this lecture, we'll go over what you'll learn and how to get the most out of this course.",
          resources: [
            { title: "Course Overview PDF", url: "#" },
            { title: "Setup Instructions", url: "#" }
          ]
        },
        { 
          title: "Setting Up Your Environment",
          completed: false,
          videoUrl: "https://sample-videos.com/video123/mp4/720/big_buck_bunny_720p_1mb.mp4",
          description: "Learn how to set up your development environment with all the necessary tools and configurations.",
          resources: [
            { title: "Development Tools List", url: "#" },
            { title: "Configuration Guide", url: "#" }
          ]
        }
      ]
    },
    {
      title: "Basic Concepts",
      lectures: [
        { 
          title: "Understanding Variables",
          completed: false,
          videoUrl: "https://sample-videos.com/video123/mp4/720/big_buck_bunny_720p_1mb.mp4",
          description: "Learn about variables, their types, and how to use them effectively in your code.",
          resources: [
            { title: "Variables Cheat Sheet", url: "#" },
            { title: "Practice Exercises", url: "#" }
          ]
        },
        { 
          title: "Control Flow",
          completed: false,
          videoUrl: "https://sample-videos.com/video123/mp4/720/big_buck_bunny_720p_1mb.mp4",
          description: "Master the basics of control flow including if statements, loops, and switch cases.",
          resources: [
            { title: "Control Flow Diagrams", url: "#" },
            { title: "Coding Challenges", url: "#" }
          ]
        }
      ]
    }
  ];

  function handleToggleSidebar() {
    isSidebarHidden = !isSidebarHidden;
  }

  function handleSelectChapter(event) {
    currentChapter = event.detail;
    currentLecture = currentChapter.lectures[0];
  }

  function handleSelectLecture(event) {
    currentLecture = event.detail;
  }
</script>

<Header />

<main>
  <div class="content-section" class:sidebar-open={!isSidebarHidden}>
    <Content
      {currentChapter}
      {currentLecture}
      on:selectLecture={handleSelectLecture}
    />
  </div>
  <Sidebar 
    {chapters}
    {currentChapter}
    isHidden={isSidebarHidden}
    on:toggleSidebar={handleToggleSidebar}
    on:selectChapter={handleSelectChapter}
  />
  <SidebarToggle 
    isHidden={isSidebarHidden}
    on:click={handleToggleSidebar}
  />
</main>

<style>

  main {
    width: 100vw;
    margin-top: var(--header-height);
    min-height: calc(100vh - var(--header-height));
    position: relative;
  }

  .content-section {
    margin: 0;
    padding: 0;
    transition: margin-right 0.3s ease;
  }

  .content-section.sidebar-open {
    margin-right: 27%;
  }

  @media (max-width: 1024px) {
    .content-section.sidebar-open {
      margin-right: 0;
    }
  }
</style>

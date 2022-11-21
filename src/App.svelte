<script>
  import FeedbackList from "./components/FeedbackList.svelte";
  import FeedbackStats from "./components/FeedbackStats.svelte";
  import FeedbackForm from "./components/FeedbackForm.svelte";
  let feedback = [];

  $: count = feedback.length;
  $: average = getAvg(feedback);

  const deleteFeedback = (event) => {
    const id = event.detail;
    feedback = feedback.filter((item) => item.id !== id);
  };

  const addFeedback = (e) => {
    const newFeedback = e.detail;
    console.log(e.detail);
    feedback = [newFeedback, ...feedback];
  };

  const getAvg = (arr) => {
    if (arr.length === 0) return 0;
    return arr.reduce((acc, curr) => acc + curr.rating, 0) / arr.length;
  };
</script>

<main class="container">
  <FeedbackForm on:add-feedback={addFeedback} />
  <FeedbackStats {count} {average} />
  <FeedbackList {feedback} on:delete-feedback={deleteFeedback} />
</main>

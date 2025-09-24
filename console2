(async function unbookmarkPosts() {
  const DELAY_BETWEEN_CLICKS_MS = 200;
  const DELAY_BETWEEN_ACTIONS_MS = 1950;
  const MAX_RETRIES = 30;

  const delay = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

  const waitForElement = async (selector, timeout = 30000) => {
    const startTime = Date.now();
    while (Date.now() - startTime < timeout) {
      const element = document.querySelector(selector);
      if (element) return element;
      await delay(130);
    }
    throw new Error(`Element with selector "${selector}" not found within ${timeout}ms`);
  };

  const clickElement = async (element) => {
    if (!element) throw new Error("Element not found");
    element.scrollIntoView({ behavior: "smooth", block: "center" });
    element.click();
  };

  try {
    // Scroll to the bottom of the page and wait 500ms
    window.scrollTo(0, document.body.scrollHeight);
    await delay(500);

    // Step 1: Click all <div class="_aagw"></div> and corresponding "Remove" buttons
    const aagwElements = document.querySelectorAll("div._aagw");
    if (aagwElements.length === 0) return;

    for (let i = 0; i < aagwElements.length; i++) {
      await clickElement(aagwElements[i]);
      await delay(DELAY_BETWEEN_CLICKS_MS);

      // Step 2: Click all <div role="button"> containing <svg aria-label="Remove"> after each _aagw click
      const removeButtons = document.querySelectorAll('div[role="button"] svg[aria-label="Remove"]');
      if (removeButtons.length === 0) continue;

      for (let j = 0; j < removeButtons.length; j++) {
        const removeButtonParent = removeButtons[j].closest('div[role="button"]');
        await clickElement(removeButtonParent);
        await delay(DELAY_BETWEEN_CLICKS_MS);
      }
      await delay(DELAY_BETWEEN_ACTIONS_MS);
    }

    // Step 3: Click all <div role="button"> containing <svg aria-label="Close">
    const closeButtons = document.querySelectorAll('div[role="button"] svg[aria-label="Close"]');
    if (closeButtons.length === 0) return;

    for (let i = 0; i < closeButtons.length; i++) {
      const closeButtonParent = closeButtons[i].closest('div[role="button"]');
      await clickElement(closeButtonParent);
      await delay(DELAY_BETWEEN_CLICKS_MS);
    }
  } catch (error) {
    window.location.href = 'https://www.instagram.com/ali_al707/saved/all-posts/';
  }
})();

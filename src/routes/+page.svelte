<script>
    let playGame = false;
    let selectedRandomText;
    let counter;

    const randomTexts = [
        "Now is the winter of our discontent Made glorious summer by this sun of York And all the clouds that lour'd upon our house In the deep bosom of the ocean buried. Now are our brows bound with victorious wreaths; Our bruised arms hung up for monuments; Our stern alarums changed to merry meetings, Our dreadful marches to delightful measures.",
        "Grim-visaged war hath smooth'd his wrinkled front; And now, instead of mounting barded steeds To fright the souls of fearful adversaries, He capers nimbly in a lady's chamber to the lascivious pleasing of a lute. But I, that am not shaped for sportive tricks, Nor made to court an amorous looking-glass; I, that am rudely stamp'd, and want love's majesty"
    ];

    const reset = () => {
        playGame = false;
    }

    const setPlayGameTrue = () => {
        selectedRandomText = randomTexts[Math.floor(Math.random() * randomTexts.length)];
        counter = 60;
        playGame = true;

        let interval = setInterval(() => {
            counter -= 1;

            if (counter === 0) {
                clearInterval(interval);

                let selectedRandomTextArray = selectedRandomText.split("");
                let typedTextArray = document.querySelector(".typing-area").value.split("");

                let charDifferences = 0;

                for (let i = 0; i < typedTextArray.length; i++) {
                    if (selectedRandomTextArray[i] !== typedTextArray[i]) {
                        charDifferences += 1;
                    }
                }

                if (typedTextArray.length < selectedRandomTextArray.length) {
                    charDifferences += selectedRandomTextArray.length - typedTextArray.length;
                }

                alert("Character Differences: " + charDifferences);

                playGame = false;
            }
        }, 1000);
    }
</script>

<main>
    <div class="main-container">
        {#if playGame}
            <div class="typing-game-container">
                <div class="counter-container">
                    <h1>{counter}</h1>
                </div>
                <div class="game-area-container">
                    <div class="textarea-container">
                        <textarea cols="40" rows="10" bind:value={selectedRandomText}></textarea> 
                    </div>
                    <div class="typing-container">
                        <input type="text" class="typing-area" autofocus>
                    </div>
                </div>
                <div class="reset-container">
                    <button on:click={reset}>Reset</button>
                </div>
            </div>
        {:else}
            <button on:click={setPlayGameTrue}>Start</button>
        {/if}
    </div>
</main>

<style>
    :global(body) {
        background-color: rgb(27, 45, 45);
        color: white;
        font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    }

    .main-container {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -60%);
    }

    .typing-game-container {
        text-align: center;
    }

    .textarea-container{
        padding: 20px;
    }

    .reset-container {
        padding-top: 20px;
    }

    button {
        background-color: black;
        color: white;
        border: none;
        border-radius: 10px;
        width: 200px;
        height: 40px;
    }

    button:hover {
        opacity: 70%;
    }

    button:active {
        opacity: 60%;
    }

    textarea {
        background-color: rgb(27, 45, 45);
        color: white;
        outline: none;
        border: 5px white solid;
        padding: 10px;
    }

    input {
        background-color: rgb(27, 45, 45);
        color: white;
        outline: none;
        border: 2px white solid;
        width: 200px;
        height: 30px;
        padding: 10px;
    }
</style>
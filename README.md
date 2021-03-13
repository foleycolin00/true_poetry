# true_poetry
Poetry generator by gpt-2 with meter and rhyme constraints. See a few examples at the bottom of this readme file.

# Setup

required imports:

come with python: string, random, math, pickle

use pip or conda to install: torch, transformers 

Python = 3.7
transformers== 3.5.1
torch==1.8.0

change transformers/trainer_pt_utils.py:37 to be 
if version.parse(torch.__version__) <= version.parse("1.4.1") or version.parse(torch.__version__) > version.parse("1.7.0"):

# Usage

Just run true_poetry.py and type or paste in some text as a prompt and it will generate a sonnet, limerick, couplets or a ballad. You should switch to 

params.model_name = "gpt2-xl"

if you want it to automatically download the 6GB neural network. Gwern's finetumed poetry model does a somewhat better job at traditional poetic style, if you have a copy. It's a bit tricky to get working, though. In the same directory where true_poetry.py is, I have a folder called "poetry." In that folder sits Gwern's pytorch_model.bin and associated small files.

I downloaded all the files in a zipped tar file using this command:

rsync --verbose rsync://78.46.86.149:873/biggan/2019-12-13-gwern-gpt-2-1.5b-poetry-model-500522.tar.xz ./ 

this is the version for tensorflow. You then have to convert it for pytorch with the following command (adjust the path as needed):

%env OPENAI_GPT2_CHECKPOINT_PATH=/content/true_poetry/gwern

!transformers-cli convert --model_type gpt2 --tf_checkpoint model-500522
--config /content/true_poetry/gwern/config.json --pytorch_dump_output /

If that's too much work, just use the gpt2-xl file, it works fine.

As for fine-tuning your own model, Gwern's post about how he did it ( https://www.gwern.net/GPT-2 ) goes into enough detail that I was able to fine tune the 345M size model. But since gpt2-xl is so much better anyway, and it is impossible to train without special hardware, you are probably going to get better results by experimenting with finding just the right prompt and sticking with one of these two models than by training your own model.

You can modify the meter or rhyme scheme however you want.

There is still some work to be done. It likes short, one-token words too much. Sometimes the rhyming word is grammatically incorrect. The longer the poem goes, the more likely it is to degenerate.

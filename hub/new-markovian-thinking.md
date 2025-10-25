New 'Markovian Thinking' technique unlocks a path to million-token AI reasoning
Ben Dickson

Researchers at Mila have proposed a new technique that makes large language models (LLMs) vastly more efficient when performing complex reasoning. Called Markovian Thinking, the approach allows LLMs to engage in lengthy reasoning without incurring the prohibitive computational costs that currently limit such tasks.

The team’s implementation, an environment named Delethink, structures the reasoning chain into fixed-size chunks, breaking the scaling problem that plagues very long LLM responses. Initial estimates show that for a 1.5B parameter model, this method can cut the costs of training by more than two-thirds compared to standard approaches.
The quadratic curse of long-chain reasoning

For an LLM to solve a complex problem, it often needs to generate a long series of intermediate “thinking” tokens, often referred to as chain-of-thought (CoT). In recent years, researchers have found that using reinforcement learning (RL) to train models to produce longer CoTs (sometimes referred to as LongCoT) has significantly improved their reasoning capabilities.

However, the standard method for this has a critical flaw: The AI's "state" (the prompt plus all the reasoning tokens it has generated thus far in its processing) grows with every new reasoning token. For modern transformer-based models, this means the computational cost explodes quadratically as the reasoning chain gets longer, making it prohibitively expensive to train models for very complex tasks.

Most current attempts to manage this cost focus on limiting how much thinking the model does, implicitly preferring shorter solutions or terminating the process early. While these methods offer some relief, the Mila researchers still operate within the LongCoT framework and are thus fundamentally bound by its quadratic nature.

Instead of trying to control the computational growth, Mila created an RL environment that avoids the quadratic problem altogether. As co-author Amirhossein Kazemnejad explained, the goal is to enable capabilities like multi-week reasoning and scientific discovery. "That regime (and the RL needed to enable such capabilities) is not supported by the current LongCoT paradigm, because of quadratic compute cost," he said.
Thinking in chunks with Delethink

The researchers' solution is a paradigm they call the "Markovian Thinker," where the model reasons while keeping the size of its reasoning context window constant. The core idea is to change the RL setup to separate "how long the model thinks" from "how much context it must process." If done correctly, a Markovian Thinker turns the quadratic growth problem into linear compute and fixed memory requirements for LLM reasoning.
Delethink vs LongCoT

How Delethink works vs LongCoT (source: arXiv)

The researchers put this paradigm into practice through Delethink, which forces the model to reason in a sequence of fixed-size chunks, such as 8,000 tokens at a time. Within each chunk, the model reasons as it normally would, using the classic attention mechanism. But when it reaches the limit of the chunk, the environment resets the context, creating a new prompt that includes the original query plus a short "carryover" from the previous chunk. For example, the carryover could be the last few tokens of the previous chunk of CoT or a summary of the most important results.

This rearrangement of the problem forces the model to learn how to embed a summary of its progress, or a "textual Markovian state," into this carryover to continue its reasoning in the next chunk. This addresses the common concern of whether the model can remember important details from earlier steps. 

According to Kazemnejad, the model learns what to remember. "With training... the model is forced to learn to carry forward the task-critical state," he explained. He added crucial clarification for practical use: The original input prompt is not modified, including the documents or contextual data added to it. “Our approach is aimed at the reasoning phase and does not modify the prompt," he said.
Delethink in action

To test their approach, the researchers trained R1-Distill-1.5B with Delethink on a dataset of competition-level math problems, then evaluated it against several benchmarks. The model was trained to reason for up to 24,000 tokens but with fixed 8,000-token chunks.
Delethink performance

Performance of Delethink on different industry benchmarks (shaded parts are extended thinking budget) (source: arXiv)

The researchers compared this to models trained with the standard LongCoT-RL method. Their findings indicate that the model trained with Delethink could reason up to 24,000 tokens, and matched or surpassed a LongCoT model trained with the same 24,000-token budget on math benchmarks. On other tasks like coding and PhD-level questions, Delethink also matched or slightly beat its LongCoT counterpart. “Overall, these results indicate that Delethink uses its thinking tokens as effectively as LongCoT-RL with reduced compute,” the researchers write.

The benefits become even more pronounced when scaling beyond the training budget. While models trained with LongCoT quickly plateaued at their training limits, the Delethink-trained model continued to improve its performance. For instance, some math problems were only solved after the model reasoned for up to 140,000 tokens, far beyond its 24,000-token training budget. This linear compute advantage is substantial for enterprise applications. The researchers estimate that training a model to an average thinking length of 96,000 tokens would require 27 H100-GPU-months with LongCoT, versus just 7 with Delethink.
Delethink training cost

Training costs of Delethink vs LongCoT (source: arXiv)

This efficiency extends directly to inference, the primary operational cost for most enterprises. "Models trained in Markovian Thinking use the same inference style (delethink-tracing) during test time, which provides the same advantages of linear compute and constant memory after training," said Kazemnejad. He offered a practical example: An AI agent could "debug a large codebase and think for a long time... which of course reduces the cost significantly compared to the conventional LongCoT approach."

Interestingly, the researchers found that off-the-shelf reasoning models, even without any specific training, already exhibit some ability to think in a Markovian way. This finding has immediate practical implications for developers. "In practice, this means that — without Delethink-RL— these models can already run a delethink-tracing wrapper and perform competitively with LongCoT on our benchmarked tasks," Kazemnejad said.

Their experiments with larger models such as GPT-OSS 120B showed robust performance with Delethink across a range of complex tasks. This latent ability provides a strong starting point for RL training, helping explain why the method is so effective. “Together, these results suggest that Delethink is compatible and scales with state-of-the-art models,” the researchers conclude.

The success of Markovian Thinking shows it may be possible for "next-generation reasoning models to think for millions of tokens," the researchers note. This opens the door to fundamentally new AI capabilities, moving beyond current constraints.

"Markovian Thinking... opens the path for models that can 'think' for very long horizons, which we view as a necessary step toward eventual scientific discovery," Kazemnejad said. "Our approach removes a key bottleneck and can allow training for much longer horizon tasks, which enables next-gen capabilities."


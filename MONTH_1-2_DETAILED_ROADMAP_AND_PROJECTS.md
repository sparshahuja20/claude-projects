# Month 1-2: Foundation Learning - Detailed Roadmap & Projects
## Complete Guide with Daily Breakdown, Code Examples & Projects

**Duration:** 8 weeks (Days 1-56)  
**Time Commitment:** 10-20 hours/week  
**Total Hours:** 100-160 hours  
**Final Deliverable:** Production-ready RAG Q&A Chatbot

---

## Table of Contents

1. [Overview](#overview)
2. [Week 1-4: LLM Basics & Theory](#week-1-4-llm-basics--theory)
3. [Week 5-8: Practical LLM Applications](#week-5-8-practical-llm-applications)
4. [Project 1: Simple Chatbot](#project-1-simple-chatbot)
5. [Project 2: RAG Q&A System](#project-2-rag-qa-system)
6. [Project 3: Vector DB Exploration](#project-3-vector-database-exploration)
7. [Project 4: LangChain Application](#project-4-langchain-application)
8. [Resources & Links](#resources--links)
9. [Progress Tracking](#progress-tracking)

---

## Overview

### Goals for Month 1-2
- ✅ Understand how transformers and LLMs work
- ✅ Learn prompt engineering principles
- ✅ Build 4 working projects
- ✅ Deploy RAG system locally
- ✅ Create GitHub portfolio with quality documentation

### Success Metrics
- [ ] Can explain attention mechanism to a colleague
- [ ] Built working chatbot with ChatGPT API
- [ ] Understanding of RAG architecture
- [ ] Deployed simple RAG system
- [ ] 4 GitHub repositories with README

### Prerequisites
- Python 3.10+ installed
- OpenAI API key
- Basic Python knowledge (you have this!)
- ~12-15 hours per week available

---

## Week 1-4: LLM Basics & Theory

### Week 1: Transformer Fundamentals (Days 1-7)

#### Daily Schedule

**Monday (Day 1): Setup & Context**
**Time:** 2 hours

**Tasks:**
1. [ ] Set up development environment
   - Python 3.10+
   - VSCode/PyCharm
   - Git repository
   - Virtual environment

```bash
# Setup
python3 -m venv venv
source venv/bin/activate  # macOS/Linux
# or: venv\Scripts\activate  # Windows

pip install jupyter notebook ipython numpy pandas
```

2. [ ] Get OpenAI API key
   - Sign up: https://platform.openai.com
   - Create API key
   - Set as environment variable

```bash
# Add to ~/.bashrc or ~/.zshrc
export OPENAI_API_KEY="sk-xxx"
```

3. [ ] Enroll in courses
   - DeepLearning.AI account
   - Fast.ai registration
   - GitHub account setup

**Deliverable:** Development environment ready, first notebook created

---

**Tuesday (Day 2): LLM Basics**
**Time:** 2.5 hours

**Reading:**
- [ ] "What is a Large Language Model?" (30 min)
  - Blog: https://www.deeplearning.ai/
- [ ] "Tokens in LLMs" explanation (20 min)
  - Read: https://platform.openai.com/tokenizer
- [ ] Watch: "Introduction to LLMs" video (60 min)

**Exercises:**
- [ ] Use OpenAI tokenizer
  - Tokenize: "Hello world how are you"
  - Tokenize: Your name
  - Tokenize: A paragraph from your resume
  - **Observation:** Count tokens in each

**Code Exercise:**
```python
import tiktoken

# Initialize tokenizer
enc = tiktoken.encoding_for_model("gpt-4")

# Tokenize text
text = "Hello world! How are you?"
tokens = enc.encode(text)

print(f"Text: {text}")
print(f"Tokens: {tokens}")
print(f"Token count: {len(tokens)}")

# Decode back
decoded = enc.decode(tokens)
print(f"Decoded: {decoded}")
```

**Deliverable:** Understand tokens and how LLMs see text

---

**Wednesday (Day 3): Attention Mechanism**
**Time:** 3 hours

**Reading:**
- [ ] "Attention is All You Need" - Intro + Section 2 (60 min)
  - Link: https://arxiv.org/abs/1706.03762
  - Focus: What is attention? Why it matters?
  
- [ ] 3Blue1Brown - Attention Mechanism video (15 min)
  - Link: https://www.youtube.com/watch?v=eMlx5aFJsqE

- [ ] Blog: "The Illustrated Transformer" (60 min)
  - Link: https://jalammar.github.io/illustrated-transformer/

**Exercises:**
- [ ] Create notes on attention mechanism
  - What is it?
  - Why is it better than RNN?
  - Query, Key, Value explained
  - Multi-head attention?

**Visual Exercise:**
```python
# Understand attention scores
import numpy as np

# Simple attention calculation
Q = np.array([[1, 0], [0, 1]])  # Queries
K = np.array([[1, 0], [0, 1]])  # Keys
V = np.array([[2, 0], [0, 2]])  # Values

# Attention scores
scores = Q @ K.T
print("Attention scores:\n", scores)

# Softmax
exp_scores = np.exp(scores)
attention_weights = exp_scores / exp_scores.sum(axis=1, keepdims=True)
print("\nAttention weights:\n", attention_weights)

# Output
output = attention_weights @ V
print("\nAttention output:\n", output)
```

**Deliverable:** Deep understanding of attention mechanism

---

**Thursday (Day 4): Transformer Architecture**
**Time:** 2.5 hours

**Reading:**
- [ ] "Attention is All You Need" - Sections 3-4 (60 min)
- [ ] Blog: "How Transformers Work" (45 min)
- [ ] Video: "Transformer Deep Dive" (30 min)

**Concepts to Master:**
- [ ] Encoder-Decoder architecture
- [ ] Multi-head attention
- [ ] Position encodings
- [ ] Feed-forward networks
- [ ] Residual connections
- [ ] Layer normalization

**Diagram Exercise:**
```
Draw the following:

1. Single Attention Head
   Input → Q,K,V → Attention Scores → Softmax → Output

2. Multi-Head Attention
   Input → 8 parallel attention heads → Concat → Linear → Output

3. Full Transformer Block
   Input → Multi-Head Attn → Add & Norm → FFN → Add & Norm → Output

4. Sequence Processing
   Token 1 → Transformer → Output 1
   Token 2 → Transformer → Output 2
   ...
```

**Deliverable:** Understand full transformer architecture

---

**Friday (Day 5): Pre-training & Fine-tuning**
**Time:** 2 hours

**Reading:**
- [ ] "How are Large Language Models Trained?" (30 min)
- [ ] "Fine-tuning vs Prompt Engineering" (30 min)
- [ ] Blog: "BERT vs GPT" (30 min)

**Key Concepts:**
- [ ] Pre-training (massive unlabeled data)
- [ ] Self-supervised learning
- [ ] Fine-tuning (labeled data)
- [ ] In-context learning
- [ ] Few-shot learning

**Code Exercise:**
```python
from transformers import pipeline, AutoTokenizer, AutoModel

# Pre-trained model loading
tokenizer = AutoTokenizer.from_pretrained("bert-base-uncased")
model = AutoModel.from_pretrained("bert-base-uncased")

# Tokenize
text = "Hello, my name is John"
tokens = tokenizer(text, return_tensors="pt")

print("Tokens:", tokens['input_ids'])

# Get embeddings
outputs = model(**tokens)
embeddings = outputs.last_hidden_state

print("Embedding shape:", embeddings.shape)
# (1, 8, 768) = (batch_size, seq_length, hidden_size)
```

**Deliverable:** Understand pre-training and fine-tuning

---

**Saturday-Sunday (Days 6-7): Review & Exercises**
**Time:** 3 hours

**Activities:**
- [ ] Re-read notes on attention
- [ ] Complete 3Blue1Brown exercises
- [ ] Write 1-page summary: "How Transformers Work"
- [ ] Answer practice questions

**Practice Questions:**
1. What is the difference between Q, K, V in attention?
2. Why do we use multi-head attention instead of single attention?
3. How does position encoding help transformers?
4. Why are transformers better than RNNs for sequences?
5. What is the difference between encoder and decoder?

**Deliverable:** Week 1 summary document with answers

---

### Week 2: Embeddings & Scaling (Days 8-14)

**Monday (Day 8): Word Embeddings**
**Time:** 2 hours

**Reading:**
- [ ] "Word Embeddings Explained" (45 min)
- [ ] "From Tokens to Embeddings" (30 min)

**Concepts:**
- [ ] Token IDs → Embedding vectors
- [ ] Semantic similarity
- [ ] Vector space representation
- [ ] Embedding dimensions
- [ ] Quality of embeddings

**Code Exercise:**
```python
import numpy as np
from sklearn.metrics.pairwise import cosine_similarity

# Simulate embeddings (real embeddings are 1536-dim for OpenAI)
embeddings = {
    "king": np.array([0.9, 0.1, 0.0]),
    "queen": np.array([0.85, 0.15, 0.0]),
    "prince": np.array([0.8, 0.05, 0.15]),
    "dog": np.array([0.1, 0.2, 0.7]),
    "cat": np.array([0.15, 0.25, 0.6]),
}

# Calculate similarities
for word1 in embeddings:
    similarities = {}
    for word2 in embeddings:
        sim = cosine_similarity(
            [embeddings[word1]], 
            [embeddings[word2]]
        )[0][0]
        similarities[word2] = round(sim, 3)
    print(f"{word1}: {similarities}")

# Output shows: king~queen, dog~cat
```

**Deliverable:** Understand how embeddings encode meaning

---

**Tuesday (Day 9): OpenAI Embeddings API**
**Time:** 2.5 hours

**Hands-on:**
- [ ] Use OpenAI embeddings API
- [ ] Compare similarity between texts
- [ ] Understand embedding dimensions

**Code Exercise:**
```python
from openai import OpenAI
from sklearn.metrics.pairwise import cosine_similarity

client = OpenAI(api_key="sk-xxx")

def get_embedding(text):
    response = client.embeddings.create(
        input=text,
        model="text-embedding-3-small"  # 1536 dimensions
    )
    return response.data[0].embedding

# Get embeddings
texts = [
    "The cat is sleeping",
    "The dog is barking",
    "A feline is resting",
    "A canine is making noise"
]

embeddings = [get_embedding(text) for text in texts]

# Calculate similarities
for i in range(len(texts)):
    for j in range(i+1, len(texts)):
        sim = cosine_similarity(
            [embeddings[i]], 
            [embeddings[j]]
        )[0][0]
        print(f"'{texts[i]}' vs '{texts[j]}': {sim:.3f}")

# Output shows semantic similarity (regardless of different words)
```

**Deliverable:** API working, understand OpenAI embeddings

---

**Wednesday (Day 10): Scaling Laws**
**Time:** 2 hours

**Reading:**
- [ ] "Scaling Laws for Neural Language Models" (60 min)
- [ ] "GPT-3 Paper" intro section (30 min)

**Concepts:**
- [ ] Model size (parameters)
- [ ] Data size (tokens)
- [ ] Compute budget
- [ ] Loss vs scale relationship
- [ ] Chinchilla scaling laws

**Key Insight:**
```
Performance improves with:
1. Model size (more parameters)
2. Training data (more tokens)
3. Compute (longer training)

Trade-off:
- Larger model = slower inference
- More data = longer training
- Optimal: balance all three
```

**Deliverable:** Understand why GPT-4 is better than GPT-3

---

**Thursday (Day 11): LLM Capabilities**
**Time:** 2 hours

**Reading:**
- [ ] "What can LLMs do?" overview (30 min)
- [ ] "Emergent abilities of LLMs" (30 min)
- [ ] "Reasoning in LLMs" (30 min)

**Topics:**
- [ ] In-context learning
- [ ] Chain-of-thought reasoning
- [ ] Few-shot vs zero-shot
- [ ] Multi-task abilities
- [ ] Limitations and failure modes

**Code Exercise:**
```python
from openai import OpenAI

client = OpenAI()

# Zero-shot learning
response = client.chat.completions.create(
    model="gpt-4",
    messages=[
        {"role": "user", "content": "Classify this as positive or negative: The movie was amazing!"}
    ]
)
print("Zero-shot:", response.choices[0].message.content)

# Few-shot learning
response = client.chat.completions.create(
    model="gpt-4",
    messages=[
        {
            "role": "user",
            "content": """
            Examples:
            "Great movie!" → Positive
            "Terrible experience" → Negative
            
            Now classify: "It was okay"
            """
        }
    ]
)
print("Few-shot:", response.choices[0].message.content)

# Chain-of-thought
response = client.chat.completions.create(
    model="gpt-4",
    messages=[
        {
            "role": "user",
            "content": "Let's think step by step: If John has 3 apples and buys 2 more, how many does he have?"
        }
    ]
)
print("Chain-of-thought:", response.choices[0].message.content)
```

**Deliverable:** Understand LLM capabilities and limitations

---

**Friday (Day 12): Safety & Limitations**
**Time:** 1.5 hours

**Reading:**
- [ ] "LLM Safety and Alignment" (30 min)
- [ ] "Hallucinations in LLMs" (30 min)

**Topics:**
- [ ] Hallucinations
- [ ] Adversarial prompts
- [ ] Biases in models
- [ ] Token limit constraints
- [ ] Safety training (RLHF)

**Deliverable:** Understand limitations you'll encounter

---

**Saturday-Sunday (Days 13-14): Week 2 Wrap-up**
**Time:** 2.5 hours

**Activities:**
- [ ] Create study notes: "Embeddings & Scaling"
- [ ] Run all code examples
- [ ] Quiz yourself on concepts
- [ ] Build Week 2 summary

**Summary Topics:**
1. How embeddings work
2. OpenAI embeddings API
3. Scaling laws and their importance
4. LLM capabilities and limitations

**Deliverable:** Week 2 summary + working code examples

---

### Week 3: Applied Learning - Prompting (Days 15-21)

**Monday (Day 15): Prompt Engineering Basics**
**Time:** 2.5 hours

**Reading:**
- [ ] "Prompt Engineering for Developers" - Introduction (45 min)
- [ ] "Principles of Prompting" (45 min)

**Key Principles:**
1. **Clarity:** Be specific and clear
2. **Context:** Provide relevant background
3. **Format:** Request specific output format
4. **Examples:** Show examples of desired output

**Code Exercise:**
```python
from openai import OpenAI

client = OpenAI()

# Bad prompt
bad_prompt = "Tell me about Python"
response = client.chat.completions.create(
    model="gpt-4",
    messages=[{"role": "user", "content": bad_prompt}]
)
print("Bad prompt result (too broad):", response.choices[0].message.content[:100])

# Good prompt
good_prompt = """
You are a Python expert teacher.
Explain Python list comprehension to a beginner in 3-4 sentences.
Include one code example.
Keep it simple and clear.
"""
response = client.chat.completions.create(
    model="gpt-4",
    messages=[{"role": "user", "content": good_prompt}]
)
print("\nGood prompt result:", response.choices[0].message.content)
```

**Deliverable:** Understand good vs bad prompts

---

**Tuesday (Day 16): Prompt Techniques**
**Time:** 2.5 hours

**Reading:**
- [ ] "Few-shot Prompting" (30 min)
- [ ] "Chain-of-Thought Prompting" (30 min)
- [ ] "Role-Based Prompting" (30 min)

**Techniques:**

1. **Few-shot Prompting:**
```python
# Before: vague
response = client.chat.completions.create(
    model="gpt-4",
    messages=[{"role": "user", "content": "Extract sentiment"}]
)

# After: with examples
response = client.chat.completions.create(
    model="gpt-4",
    messages=[{
        "role": "user",
        "content": """
        Extract sentiment from text:
        
        Text: "The food was great!" → Sentiment: Positive
        Text: "I hated it" → Sentiment: Negative
        Text: "It was okay" → Sentiment: Neutral
        
        Now extract: "Best movie ever!"
        """
    }]
)
```

2. **Chain-of-Thought:**
```python
response = client.chat.completions.create(
    model="gpt-4",
    messages=[{
        "role": "user",
        "content": """
        Think step by step:
        
        Problem: If there are 8 oranges and I eat 2, then give 3 away, how many are left?
        
        Step 1: Start with 8 oranges
        Step 2: Eat 2 → 8 - 2 = 6 left
        Step 3: Give away 3 → 6 - 3 = 3 left
        Answer: 3 oranges
        
        Now solve: I have 5 apples, buy 3 more, eat 1. How many do I have?
        """
    }]
)
```

3. **Role-Based Prompting:**
```python
response = client.chat.completions.create(
    model="gpt-4",
    messages=[{
        "role": "user",
        "content": """
        You are a professional Python code reviewer.
        Review this code for potential improvements:
        
        def add(a, b):
            return a + b
        
        Focus on: readability, efficiency, and best practices.
        """
    }]
)
```

**Deliverable:** Master prompting techniques

---

**Wednesday (Day 17): Prompt Optimization**
**Time:** 2 hours

**Reading:**
- [ ] "Iteratively Improving Prompts" (45 min)
- [ ] "Prompt Engineering Best Practices" (45 min)

**Optimization Process:**
```
1. Start with basic prompt
2. Run it 5-10 times
3. Analyze outputs (consistency, quality)
4. Identify issues
5. Refine prompt
6. Repeat steps 2-5
```

**Code Exercise:**
```python
from openai import OpenAI

client = OpenAI()

# Prompt versions
prompts = {
    "v1": "Extract entities from: The Eiffel Tower is in France",
    
    "v2": """
    Extract named entities (people, places, organizations) from text.
    Format: Entity | Type
    
    Text: The Eiffel Tower is in France
    """,
    
    "v3": """
    You are a named entity recognition (NER) system.
    Extract all named entities from the text and classify them.
    
    Categories:
    - LOCATION: Cities, countries, landmarks
    - PERSON: Names of people
    - ORGANIZATION: Companies, institutions
    
    Format output as:
    Entity | Type | Confidence
    
    Text: The Eiffel Tower is in France
    
    Only extract entities with high confidence.
    """
}

for version, prompt in prompts.items():
    response = client.chat.completions.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}]
    )
    print(f"\n{version}:")
    print(response.choices[0].message.content)
```

**Deliverable:** Understand how to iterate on prompts

---

**Thursday (Day 18): Advanced Prompting**
**Time:** 2 hours

**Reading:**
- [ ] "Self-Consistency Prompting" (30 min)
- [ ] "Tree-of-Thought Prompting" (30 min)

**Advanced Techniques:**

1. **Self-Consistency:**
```python
# Ask question multiple times with slight variation
# Then find most consistent answer

def get_answer_with_consistency(question, num_attempts=3):
    responses = []
    for _ in range(num_attempts):
        response = client.chat.completions.create(
            model="gpt-4",
            messages=[{
                "role": "user",
                "content": f"{question}\nLet's think step by step."
            }],
            temperature=0.7  # Add randomness
        )
        responses.append(response.choices[0].message.content)
    
    # Find most consistent answer
    return responses

# Use it
answers = get_answer_with_consistency("What is 7+8?")
# Run multiple times to see consistency
```

2. **Prompt Chaining:**
```python
# Break complex task into multiple prompts

def extract_and_summarize(text):
    # Step 1: Extract key points
    step1_response = client.chat.completions.create(
        model="gpt-4",
        messages=[{
            "role": "user",
            "content": f"Extract 3 key points: {text}"
        }]
    )
    key_points = step1_response.choices[0].message.content
    
    # Step 2: Summarize key points
    step2_response = client.chat.completions.create(
        model="gpt-4",
        messages=[{
            "role": "user",
            "content": f"Create a concise summary from these points: {key_points}"
        }]
    )
    
    return step2_response.choices[0].message.content

# Use it
summary = extract_and_summarize("Long article text here...")
```

**Deliverable:** Understand advanced prompting techniques

---

**Friday (Day 19): Prompt Engineering Best Practices**
**Time:** 1.5 hours

**Checklist for Good Prompts:**
- [ ] Clear and specific
- [ ] Provides context
- [ ] Specifies output format
- [ ] Includes examples (few-shot)
- [ ] Has appropriate role definition
- [ ] Uses step-by-step thinking when needed
- [ ] Handles edge cases

**Code Exercise:**
```python
# Create a prompt template library

prompt_templates = {
    "classify": """
    You are a sentiment classification expert.
    Classify the following text as Positive, Negative, or Neutral.
    
    Text: {text}
    
    Output format: Sentiment: [Your answer]
    Confidence: [0-100]
    """,
    
    "extract": """
    Extract {entity_type} from the text.
    
    Text: {text}
    
    Format: One per line
    """,
    
    "generate": """
    You are a {role}.
    Generate {what} about {topic}.
    
    Requirements:
    - Length: {length}
    - Tone: {tone}
    - Format: {format}
    """,
}

# Use template
from string import Template

classifier = prompt_templates["classify"]
prompt = classifier.format(text="This movie was amazing!")
print(prompt)
```

**Deliverable:** Reusable prompt templates

---

**Saturday-Sunday (Days 20-21): Week 3 Projects**
**Time:** 4 hours

**Project: Prompt Testing Framework**

Create a script to test different prompts:

```python
from openai import OpenAI
import json

client = OpenAI()

class PromptTester:
    def __init__(self):
        self.results = []
    
    def test_prompt(self, name, prompt, num_runs=3):
        """Test a prompt multiple times"""
        outputs = []
        
        for i in range(num_runs):
            response = client.chat.completions.create(
                model="gpt-4",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.7
            )
            output = response.choices[0].message.content
            outputs.append(output)
        
        result = {
            "name": name,
            "prompt": prompt,
            "outputs": outputs,
            "num_runs": num_runs
        }
        self.results.append(result)
        return result
    
    def compare_prompts(self, prompts_dict):
        """Compare multiple prompts"""
        for name, prompt in prompts_dict.items():
            self.test_prompt(name, prompt, num_runs=2)
        
        return self.results
    
    def save_results(self, filename="prompt_test_results.json"):
        """Save results to file"""
        with open(filename, 'w') as f:
            json.dump(self.results, f, indent=2)

# Use it
tester = PromptTester()

prompts = {
    "basic": "What is machine learning?",
    "detailed": """
    Explain machine learning to a non-technical person in 2-3 sentences.
    Include one real-world example.
    """,
    "expert": """
    You are a machine learning expert.
    Explain supervised learning with:
    1. Definition
    2. Key algorithms
    3. Real-world applications
    """
}

tester.compare_prompts(prompts)
tester.save_results()

# Review results
for result in tester.results:
    print(f"\n{result['name']}:")
    for i, output in enumerate(result['outputs']):
        print(f"  Run {i+1}: {output[:100]}...")
```

**Deliverable:** Working prompt testing framework

---

### Week 4: Practical Applications (Days 22-28)

**Monday (Day 22): OpenAI API Deep Dive**
**Time:** 2 hours

**Topics:**
- [ ] Different models (GPT-4, GPT-3.5, etc.)
- [ ] Temperature and top_p parameters
- [ ] Max tokens
- [ ] Cost optimization
- [ ] Rate limiting

**Code Exercise:**
```python
from openai import OpenAI
import time

client = OpenAI()

# Model comparison
models = {
    "gpt-4": {
        "input_cost": 0.03,
        "output_cost": 0.06,
        "capabilities": "Best quality, slowest"
    },
    "gpt-3.5-turbo": {
        "input_cost": 0.0005,
        "output_cost": 0.0015,
        "capabilities": "Fast, cheaper"
    }
}

# Temperature effects (creativity)
def test_temperature(prompt, temperatures=[0, 0.5, 1.0]):
    """Test different temperature values"""
    print(f"Testing different temperatures for: {prompt[:30]}...\n")
    
    for temp in temperatures:
        response = client.chat.completions.create(
            model="gpt-4",
            messages=[{"role": "user", "content": prompt}],
            temperature=temp,
            max_tokens=50
        )
        
        print(f"Temperature {temp}:")
        print(f"  {response.choices[0].message.content}\n")

# Test it
test_temperature("Complete this: The future of AI is...")

# Cost calculator
def calculate_cost(prompt, response_text, model="gpt-3.5-turbo"):
    """Calculate API cost"""
    input_tokens = len(prompt.split()) * 1.3  # Rough estimate
    output_tokens = len(response_text.split()) * 1.3
    
    if model == "gpt-4":
        cost = (input_tokens * 0.03 + output_tokens * 0.06) / 1000
    else:
        cost = (input_tokens * 0.0005 + output_tokens * 0.0015) / 1000
    
    return cost

print(f"Estimated cost: ${calculate_cost('What is AI?', 'AI is...'):0.4f}")
```

**Deliverable:** Understand API parameters and costs

---

**Tuesday (Day 23): Building Your First App**
**Time:** 2.5 hours

**Project: Simple Q&A App**

```python
from openai import OpenAI
import json
from datetime import datetime

client = OpenAI()

class SimpleQAApp:
    def __init__(self, system_prompt="You are a helpful assistant."):
        self.system_prompt = system_prompt
        self.conversation_history = []
    
    def ask(self, question):
        """Ask a single question"""
        response = client.chat.completions.create(
            model="gpt-3.5-turbo",
            messages=[
                {"role": "system", "content": self.system_prompt},
                {"role": "user", "content": question}
            ]
        )
        
        answer = response.choices[0].message.content
        
        # Log conversation
        self.conversation_history.append({
            "timestamp": datetime.now().isoformat(),
            "question": question,
            "answer": answer,
            "model": "gpt-3.5-turbo"
        })
        
        return answer
    
    def ask_with_context(self, question):
        """Ask question with conversation context"""
        messages = [{"role": "system", "content": self.system_prompt}]
        
        # Add previous messages
        for msg in self.conversation_history[-4:]:  # Last 4 exchanges
            messages.append({"role": "user", "content": msg["question"]})
            messages.append({"role": "assistant", "content": msg["answer"]})
        
        # Add current question
        messages.append({"role": "user", "content": question})
        
        response = client.chat.completions.create(
            model="gpt-3.5-turbo",
            messages=messages
        )
        
        answer = response.choices[0].message.content
        
        self.conversation_history.append({
            "timestamp": datetime.now().isoformat(),
            "question": question,
            "answer": answer
        })
        
        return answer
    
    def save_history(self, filename="qa_history.json"):
        """Save conversation history"""
        with open(filename, 'w') as f:
            json.dump(self.conversation_history, f, indent=2)
    
    def clear_history(self):
        """Clear conversation history"""
        self.conversation_history = []

# Use it
qa_app = SimpleQAApp(system_prompt="You are a Python expert. Answer only Python questions.")

# Single exchange
answer1 = qa_app.ask("What is a list comprehension?")
print(f"Q: What is a list comprehension?\nA: {answer1}\n")

# Contextual exchange
answer2 = qa_app.ask("Can you give me an example?")
print(f"Q: Can you give me an example?\nA: {answer2}\n")

answer3 = qa_app.ask("How is this better than a loop?")
print(f"Q: How is this better than a loop?\nA: {answer3}\n")

# Save history
qa_app.save_history()
```

**Deliverable:** Working single-turn and multi-turn Q&A app

---

**Wednesday (Day 24): Error Handling & Best Practices**
**Time:** 2 hours

**Topics:**
- [ ] Handling API errors
- [ ] Retry logic
- [ ] Rate limit handling
- [ ] Logging
- [ ] Input validation

**Code Exercise:**
```python
from openai import OpenAI, APIError, RateLimitError, APIConnectionError
import time
import logging

# Setup logging
logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

client = OpenAI()

class RobustQAApp:
    def __init__(self, max_retries=3):
        self.max_retries = max_retries
    
    def ask_with_retry(self, question):
        """Ask with automatic retry"""
        for attempt in range(self.max_retries):
            try:
                # Validate input
                if not question or len(question) > 2000:
                    raise ValueError("Question must be 1-2000 characters")
                
                logger.info(f"Attempt {attempt+1}/{self.max_retries}")
                
                response = client.chat.completions.create(
                    model="gpt-3.5-turbo",
                    messages=[{"role": "user", "content": question}]
                )
                
                logger.info(f"Success on attempt {attempt+1}")
                return response.choices[0].message.content
            
            except RateLimitError:
                logger.warning("Rate limit hit, retrying...")
                if attempt < self.max_retries - 1:
                    time.sleep(2 ** attempt)  # Exponential backoff
                    continue
                else:
                    logger.error("Max retries exceeded")
                    raise
            
            except APIConnectionError:
                logger.warning("Connection error, retrying...")
                if attempt < self.max_retries - 1:
                    time.sleep(2 ** attempt)
                    continue
                else:
                    raise
            
            except APIError as e:
                logger.error(f"API error: {e}")
                raise
            
            except ValueError as e:
                logger.error(f"Input validation error: {e}")
                raise
        
        raise Exception("Failed after all retries")

# Use it
app = RobustQAApp()
answer = app.ask_with_retry("What is machine learning?")
print(answer)
```

**Deliverable:** Production-ready error handling

---

**Thursday (Day 25): Advanced Concepts**
**Time:** 2 hours

**Topics:**
- [ ] System prompts for role definition
- [ ] Function calling (if using compatible model)
- [ ] Streaming responses
- [ ] Structured outputs

**Code Exercise:**
```python
from openai import OpenAI

client = OpenAI()

# System prompt for role definition
def expert_qa(topic, question):
    """Ask question to topic expert"""
    response = client.chat.completions.create(
        model="gpt-4",
        messages=[
            {
                "role": "system",
                "content": f"You are a world-class expert in {topic}. Explain complex concepts clearly and provide practical examples."
            },
            {"role": "user", "content": question}
        ]
    )
    return response.choices[0].message.content

# Streaming (for long responses)
def stream_answer(question):
    """Stream response for real-time display"""
    with client.chat.completions.create(
        model="gpt-4",
        messages=[{"role": "user", "content": question}],
        stream=True
    ) as stream:
        for text in stream.text_stream:
            print(text, end="", flush=True)
        print()

# Use it
print("Expert mode:")
answer = expert_qa("machine learning", "Explain neural networks")
print(answer[:200] + "...\n")

print("Streaming mode:")
stream_answer("Write a haiku about AI")
```

**Deliverable:** Advanced API features working

---

**Friday (Day 26): Week 4 Review & Project Planning**
**Time:** 1.5 hours

**Activities:**
- [ ] Review all Week 1-4 concepts
- [ ] Create comprehensive notes
- [ ] Plan Week 5 RAG project
- [ ] Set up GitHub repository

**Create a GitHub Repository:**
```bash
# Initialize repo
git init llm-learning
cd llm-learning

# Create structure
mkdir -p week1-foundations week2-embeddings week3-prompting week4-applications
mkdir notebooks code tests

# Create initial files
touch README.md requirements.txt .gitignore
```

**README structure:**
```markdown
# LLM Learning Journey

## Week 1-4: Foundations
- [Week 1: Transformers](#week-1)
- [Week 2: Embeddings](#week-2)
- [Week 3: Prompting](#week-3)
- [Week 4: Applications](#week-4)

## Projects
1. Simple Chatbot
2. Q&A Application
3. Prompt Testing Framework

## Resources
- [Course Links](#resources)
- [Key Papers](#papers)
```

**Deliverable:** Clean GitHub repo with documentation

---

**Saturday-Sunday (Days 27-28): Month 1 Wrap-up**
**Time:** 3 hours

**Activities:**
- [ ] Complete all Week 1-4 code exercises
- [ ] Write Month 1 summary
- [ ] Create quiz on all topics
- [ ] Plan Month 2 RAG projects

**Month 1 Summary Document:**
```markdown
# Month 1: Foundations - Complete Summary

## Topics Mastered
1. Transformer Architecture
   - Attention mechanisms
   - Multi-head attention
   - Position encodings

2. Embeddings & Scaling
   - Token embeddings
   - Semantic similarity
   - Scaling laws

3. Prompt Engineering
   - Few-shot learning
   - Chain-of-thought
   - Prompt optimization

4. API Applications
   - OpenAI API
   - Error handling
   - Cost optimization

## Skills Acquired
- [ ] Understand LLM fundamentals
- [ ] Can explain attention mechanism
- [ ] Can write effective prompts
- [ ] Can build simple Q&A apps

## Projects Completed
1. ✅ Tokenization experiments
2. ✅ Embedding similarity search
3. ✅ Prompt testing framework
4. ✅ Simple Q&A application

## GitHub Status
- Repository: llm-learning
- Commits: 15+
- Files: 20+
- Documentation: Complete

## Ready for Week 5
- Understanding is solid
- Confidence: High
- Next: RAG systems
```

**Deliverable:** Complete Month 1 documentation

---

## Week 5-8: Practical LLM Applications

### Week 5: RAG Foundations (Days 29-35)

**Monday (Day 29): What is RAG?**
**Time:** 2 hours

**Reading:**
- [ ] "Retrieval-Augmented Generation" paper intro (45 min)
- [ ] Blog: "RAG Explained" (45 min)

**Key Concept:**
```
Traditional LLM:
Input → Model → Output

RAG System:
Input → Retrieve relevant docs → Model → Output
         (from vector DB)
```

**Code Exercise:**
```python
from openai import OpenAI

client = OpenAI()

# Traditional LLM (limited knowledge)
def traditional_qa(question):
    response = client.chat.completions.create(
        model="gpt-4",
        messages=[{"role": "user", "content": question}]
    )
    return response.choices[0].message.content

# RAG approach
def rag_qa(question, relevant_documents):
    """
    RAG: Use retrieved documents to enhance answer
    """
    context = "\n".join(relevant_documents)
    
    response = client.chat.completions.create(
        model="gpt-4",
        messages=[
            {
                "role": "system",
                "content": "Answer based on the provided documents."
            },
            {
                "role": "user",
                "content": f"Documents:\n{context}\n\nQuestion: {question}"
            }
        ]
    )
    return response.choices[0].message.content

# Example
docs = [
    "Claude is an AI assistant made by Anthropic.",
    "Anthropic is an AI safety company founded in 2021.",
]

question = "Who made Claude?"
answer = rag_qa(question, docs)
print(answer)
```

**Deliverable:** Understand RAG concept

---

**Tuesday (Day 30): Vector Databases**
**Time:** 2.5 hours

**Topics:**
- [ ] What are vector databases?
- [ ] Pinecone, Weaviate, Milvus
- [ ] Embedding storage
- [ ] Similarity search
- [ ] Indexing strategies

**Code Exercise:**
```python
import numpy as np
from sklearn.metrics.pairwise import cosine_similarity

# Simulate vector database
class SimpleVectorDB:
    def __init__(self, dimension=1536):
        self.vectors = []
        self.metadata = []
        self.dimension = dimension
    
    def add(self, vector, metadata):
        """Add vector to database"""
        if len(vector) != self.dimension:
            raise ValueError(f"Vector must be {self.dimension} dimensions")
        
        self.vectors.append(vector)
        self.metadata.append(metadata)
    
    def search(self, query_vector, k=3):
        """Find k most similar vectors"""
        if not self.vectors:
            return []
        
        # Calculate similarities
        similarities = cosine_similarity(
            [query_vector],
            self.vectors
        )[0]
        
        # Get top k
        top_indices = np.argsort(similarities)[::-1][:k]
        
        results = []
        for idx in top_indices:
            results.append({
                "metadata": self.metadata[idx],
                "similarity": similarities[idx]
            })
        
        return results

# Use it
db = SimpleVectorDB(dimension=3)

# Add documents
documents = {
    "Claude is an AI assistant": np.array([0.9, 0.1, 0.0]),
    "Python is a programming language": np.array([0.1, 0.9, 0.0]),
    "AI is transforming technology": np.array([0.8, 0.2, 0.5]),
}

for text, vector in documents.items():
    db.add(vector, text)

# Search
query = np.array([0.85, 0.15, 0.0])  # Similar to "Claude"
results = db.search(query, k=2)

print("Search results:")
for result in results:
    print(f"  {result['metadata']} (similarity: {result['similarity']:.2f})")
```

**Deliverable:** Understand vector database basics

---

**Wednesday (Day 31): Pinecone Integration**
**Time:** 2.5 hours

**Setup:**
- [ ] Create Pinecone account: https://www.pinecone.io
- [ ] Create API key
- [ ] Create index

**Code Exercise:**
```python
from pinecone import Pinecone
from openai import OpenAI

# Initialize
pc = Pinecone(api_key="your-key")
client = OpenAI()

class PineconeRAG:
    def __init__(self, index_name="documents"):
        self.index = pc.Index(index_name)
        self.dimension = 1536  # OpenAI embedding dimension
    
    def embed_text(self, text):
        """Convert text to embedding"""
        response = client.embeddings.create(
            input=text,
            model="text-embedding-3-small"
        )
        return response.data[0].embedding
    
    def add_document(self, text, doc_id, metadata=None):
        """Add document to Pinecone"""
        embedding = self.embed_text(text)
        
        self.index.upsert(
            vectors=[
                {
                    "id": doc_id,
                    "values": embedding,
                    "metadata": {
                        "text": text,
                        **(metadata or {})
                    }
                }
            ]
        )
    
    def search(self, query_text, k=3):
        """Search for similar documents"""
        query_embedding = self.embed_text(query_text)
        
        results = self.index.query(
            vector=query_embedding,
            top_k=k,
            include_metadata=True
        )
        
        return results

# Use it
rag = PineconeRAG()

# Add documents
documents = [
    ("Claude is an AI assistant", "doc1"),
    ("Anthropic builds safe AI", "doc2"),
    ("LLMs use transformers", "doc3"),
]

for text, doc_id in documents:
    rag.add_document(text, doc_id)

# Search
results = rag.search("Tell me about Claude")
print("Search results:")
for match in results.matches:
    print(f"  {match.metadata['text']} (score: {match.score:.2f})")
```

**Deliverable:** Pinecone integration working

---

**Thursday (Day 32): LangChain Basics**
**Time:** 2.5 hours

**Topics:**
- [ ] What is LangChain?
- [ ] Key components
- [ ] Building chains
- [ ] Agents

**Installation:**
```bash
pip install langchain openai pinecone-client
```

**Code Exercise:**
```python
from langchain.embeddings.openai import OpenAIEmbeddings
from langchain.vectorstores import Pinecone
from langchain.chat_models import ChatOpenAI
from langchain.chains import RetrievalQA
import pinecone

# Initialize
embeddings = OpenAIEmbeddings()
llm = ChatOpenAI(model_name="gpt-4", temperature=0)

# Create vector store
pinecone.init(api_key="xxx", environment="us-west1-gcp")
vectorstore = Pinecone.from_texts(
    [
        "Claude is an AI assistant by Anthropic",
        "LLMs learn from large amounts of text",
        "Transformers use attention mechanisms"
    ],
    embeddings,
    index_name="langchain-docs"
)

# Create RAG chain
qa = RetrievalQA.from_chain_type(
    llm=llm,
    chain_type="stuff",
    retriever=vectorstore.as_retriever()
)

# Ask questions
answer = qa.run("What is Claude?")
print(f"Answer: {answer}")
```

**Deliverable:** LangChain RAG system working

---

**Friday (Day 33): Advanced RAG**
**Time:** 2 hours

**Topics:**
- [ ] Document chunking strategies
- [ ] Re-ranking
- [ ] Metadata filtering
- [ ] Hybrid search

**Code Exercise:**
```python
from langchain.text_splitter import RecursiveCharacterTextSplitter

class AdvancedRAG:
    def __init__(self, chunk_size=512, chunk_overlap=50):
        self.splitter = RecursiveCharacterTextSplitter(
            chunk_size=chunk_size,
            chunk_overlap=chunk_overlap,
            separators=["\n\n", "\n", ".", " "]
        )
    
    def chunk_document(self, text):
        """Split document into chunks"""
        chunks = self.splitter.split_text(text)
        return chunks
    
    def add_with_metadata(self, text, source, doc_type):
        """Add document with metadata"""
        chunks = self.chunk_document(text)
        
        documents_with_metadata = [
            {
                "content": chunk,
                "source": source,
                "type": doc_type,
                "chunk_id": i
            }
            for i, chunk in enumerate(chunks)
        ]
        
        return documents_with_metadata

# Use it
rag = AdvancedRAG()

long_document = """
Claude is an AI assistant made by Anthropic.
Anthropic is founded in 2021 with a focus on AI safety.
Claude can help with writing, analysis, and coding.
"""

docs = rag.add_with_metadata(
    long_document,
    source="anthropic-docs",
    doc_type="product-info"
)

print(f"Created {len(docs)} chunks:")
for doc in docs:
    print(f"  - {doc['content'][:50]}... (source: {doc['source']})")
```

**Deliverable:** Advanced RAG concepts

---

**Saturday-Sunday (Days 34-35): Week 5 Projects**
**Time:** 4 hours

**Project: Document Ingestion Pipeline**

```python
import os
import json
from typing import List
from langchain.embeddings.openai import OpenAIEmbeddings
from langchain.vectorstores import Pinecone
from langchain.document_loaders import TextLoader
from langchain.text_splitter import RecursiveCharacterTextSplitter

class DocumentProcessor:
    def __init__(self, chunk_size=512, chunk_overlap=50):
        self.embeddings = OpenAIEmbeddings()
        self.splitter = RecursiveCharacterTextSplitter(
            chunk_size=chunk_size,
            chunk_overlap=chunk_overlap
        )
        self.processed_docs = []
    
    def load_documents(self, directory: str) -> List[str]:
        """Load all text files from directory"""
        documents = []
        
        for filename in os.listdir(directory):
            if filename.endswith('.txt'):
                filepath = os.path.join(directory, filename)
                try:
                    with open(filepath, 'r') as f:
                        content = f.read()
                        documents.append({
                            "filename": filename,
                            "content": content
                        })
                    print(f"Loaded: {filename}")
                except Exception as e:
                    print(f"Error loading {filename}: {e}")
        
        return documents
    
    def process_documents(self, documents: List[dict]) -> List[dict]:
        """Process and chunk documents"""
        processed = []
        
        for doc in documents:
            chunks = self.splitter.split_text(doc["content"])
            
            for i, chunk in enumerate(chunks):
                processed.append({
                    "source": doc["filename"],
                    "chunk_id": i,
                    "content": chunk,
                    "chunk_count": len(chunks)
                })
        
        self.processed_docs = processed
        print(f"Processed into {len(processed)} chunks")
        return processed
    
    def save_processed(self, output_file="processed_docs.json"):
        """Save processed documents"""
        with open(output_file, 'w') as f:
            json.dump(self.processed_docs, f, indent=2)
        print(f"Saved to {output_file}")
    
    def get_stats(self):
        """Get processing statistics"""
        total_chunks = len(self.processed_docs)
        total_chars = sum(len(doc["content"]) for doc in self.processed_docs)
        total_docs = len(set(doc["source"] for doc in self.processed_docs))
        
        return {
            "total_documents": total_docs,
            "total_chunks": total_chunks,
            "total_characters": total_chars,
            "avg_chunk_size": total_chars / max(1, total_chunks)
        }

# Use it
processor = DocumentProcessor()

# Load documents
docs = processor.load_documents("./documents/")

# Process
processed = processor.process_documents(docs)

# Save
processor.save_processed()

# Stats
stats = processor.get_stats()
print(f"\nStatistics: {stats}")
```

**Deliverable:** Document ingestion pipeline

---

### Week 6: Building RAG Systems (Days 36-42)

**Monday (Day 36): Complete RAG System Design**
**Time:** 2.5 hours

**Architecture:**
```
User Query
    ↓
Embedding
    ↓
Vector DB Search
    ↓
Retrieve Top Documents
    ↓
Rerank (optional)
    ↓
Format Context
    ↓
LLM Generation
    ↓
Return Answer
```

**Code Exercise:**
```python
from openai import OpenAI
from langchain.embeddings.openai import OpenAIEmbeddings
from langchain.vectorstores import Pinecone
from langchain.chat_models import ChatOpenAI
from langchain.chains import RetrievalQA
import pinecone

class CompleteRAGSystem:
    def __init__(self, index_name="documents"):
        self.embeddings = OpenAIEmbeddings()
        self.llm = ChatOpenAI(model_name="gpt-4", temperature=0)
        
        # Initialize Pinecone
        pinecone.init(api_key="xxx", environment="us-west1-gcp")
        self.vectorstore = Pinecone.Index(index_name)
    
    def prepare_documents(self, documents: list):
        """Prepare and embed documents"""
        # Create vectorstore
        from langchain.document_loaders import TextLoader
        from langchain.text_splitter import RecursiveCharacterTextSplitter
        
        splitter = RecursiveCharacterTextSplitter(
            chunk_size=512,
            chunk_overlap=50
        )
        
        texts = []
        for doc in documents:
            if isinstance(doc, dict):
                texts.append(doc['content'])
            else:
                texts.append(doc)
        
        Pinecone.from_texts(
            texts,
            self.embeddings,
            index_name="documents"
        )
    
    def answer_question(self, question: str, context_count: int = 3):
        """Answer question using RAG"""
        # Retrieve documents
        retriever = self.vectorstore.as_retriever(search_kwargs={"k": context_count})
        
        # Create QA chain
        qa_chain = RetrievalQA.from_chain_type(
            llm=self.llm,
            chain_type="stuff",
            retriever=retriever,
            return_source_documents=True
        )
        
        # Get answer
        result = qa_chain({"query": question})
        
        return {
            "answer": result["result"],
            "source_documents": result["source_documents"]
        }
    
    def answer_with_feedback(self, question: str):
        """Answer with user feedback option"""
        result = self.answer_question(question)
        
        return {
            "question": question,
            "answer": result["answer"],
            "sources": [doc.metadata.get("source", "unknown") for doc in result["source_documents"]],
            "helpful": None  # Will be filled with user feedback
        }

# Use it
rag = CompleteRAGSystem()

question = "What is RAG?"
response = rag.answer_with_feedback(question)

print(f"Q: {response['question']}")
print(f"A: {response['answer']}")
print(f"Sources: {response['sources']}")
```

**Deliverable:** Complete RAG system architecture

---

**Tuesday-Friday (Days 37-41): Build RAG Chatbot**
**Time:** 12 hours total

**Major Project: Production RAG Chatbot**

```python
import os
import json
from datetime import datetime
from typing import Optional
from pathlib import Path

from openai import OpenAI
from langchain.embeddings.openai import OpenAIEmbeddings
from langchain.vectorstores import Pinecone
from langchain.chat_models import ChatOpenAI
from langchain.chains import RetrievalQA
import pinecone

class ProductionRAGChatbot:
    def __init__(
        self,
        index_name: str = "chatbot-docs",
        model: str = "gpt-4",
        temperature: float = 0.7,
        context_count: int = 3
    ):
        self.index_name = index_name
        self.model = model
        self.temperature = temperature
        self.context_count = context_count
        
        # Initialize components
        self.embeddings = OpenAIEmbeddings()
        self.llm = ChatOpenAI(model_name=model, temperature=temperature)
        self.client = OpenAI()
        
        # Initialize Pinecone
        pinecone.init(api_key=os.getenv("PINECONE_API_KEY"))
        
        # Conversation history
        self.conversation_history = []
        self.conversation_id = self.generate_id()
    
    def generate_id(self) -> str:
        """Generate unique conversation ID"""
        return f"conv_{datetime.now().strftime('%Y%m%d_%H%M%S')}"
    
    def add_documents(self, documents: list, metadata: Optional[dict] = None):
        """Add documents to vector store"""
        try:
            self.vectorstore = Pinecone.from_texts(
                [doc.get("content", doc) if isinstance(doc, dict) else doc 
                 for doc in documents],
                self.embeddings,
                index_name=self.index_name,
                metadatas=metadata or {}
            )
            print(f"✓ Added {len(documents)} documents to index '{self.index_name}'")
        except Exception as e:
            print(f"✗ Error adding documents: {e}")
            raise
    
    def retrieve_context(self, query: str) -> list:
        """Retrieve relevant documents"""
        try:
            retriever = self.vectorstore.as_retriever(
                search_kwargs={"k": self.context_count}
            )
            docs = retriever.get_relevant_documents(query)
            return docs
        except Exception as e:
            print(f"✗ Retrieval error: {e}")
            return []
    
    def format_context(self, documents: list) -> str:
        """Format retrieved documents as context"""
        if not documents:
            return "No relevant documents found."
        
        context = "Relevant Information:\n" + "="*50 + "\n\n"
        
        for i, doc in enumerate(documents, 1):
            content = doc.page_content if hasattr(doc, 'page_content') else str(doc)
            metadata = getattr(doc, 'metadata', {})
            source = metadata.get('source', 'Unknown source')
            
            context += f"Document {i} (from {source}):\n"
            context += f"{content}\n\n"
        
        return context
    
    def generate_answer(self, query: str, context: str) -> str:
        """Generate answer using LLM"""
        try:
            messages = [
                {
                    "role": "system",
                    "content": """You are a helpful AI assistant. 
                    Answer based on the provided context.
                    If the context doesn't contain relevant information, 
                    say so clearly.
                    Be concise and accurate."""
                },
                {
                    "role": "user",
                    "content": f"{context}\n\nQuestion: {query}"
                }
            ]
            
            # Add conversation history for context
            for msg in self.conversation_history[-4:]:
                if msg["role"] in ["user", "assistant"]:
                    messages.insert(-1, msg)
            
            response = self.client.chat.completions.create(
                model=self.model,
                messages=messages,
                temperature=self.temperature,
                max_tokens=500
            )
            
            answer = response.choices[0].message.content
            return answer
        
        except Exception as e:
            return f"Error generating answer: {str(e)}"
    
    def ask(self, query: str) -> dict:
        """Main interaction method"""
        # Retrieve context
        docs = self.retrieve_context(query)
        context = self.format_context(docs)
        
        # Generate answer
        answer = self.generate_answer(query, context)
        
        # Store in history
        exchange = {
            "timestamp": datetime.now().isoformat(),
            "user_query": query,
            "assistant_answer": answer,
            "context_sources": len(docs)
        }
        
        self.conversation_history.append({
            "role": "user",
            "content": query
        })
        self.conversation_history.append({
            "role": "assistant",
            "content": answer
        })
        
        return exchange
    
    def save_conversation(self, filename: Optional[str] = None):
        """Save conversation to file"""
        filename = filename or f"conversation_{self.conversation_id}.json"
        
        data = {
            "conversation_id": self.conversation_id,
            "model": self.model,
            "created_at": datetime.now().isoformat(),
            "exchanges": self.conversation_history
        }
        
        with open(filename, 'w') as f:
            json.dump(data, f, indent=2)
        
        print(f"✓ Conversation saved to {filename}")
        return filename
    
    def get_statistics(self) -> dict:
        """Get conversation statistics"""
        return {
            "conversation_id": self.conversation_id,
            "total_exchanges": len(self.conversation_history) // 2,
            "total_tokens_approx": sum(
                len(msg.get("content", "").split()) 
                for msg in self.conversation_history
            ) * 1.3,
            "model_used": self.model
        }

# Example Usage
if __name__ == "__main__":
    # Initialize chatbot
    chatbot = ProductionRAGChatbot(
        index_name="tutorial-docs",
        model="gpt-4",
        temperature=0.7
    )
    
    # Sample documents
    sample_docs = [
        {
            "content": "Claude is an AI assistant made by Anthropic. It can help with writing, analysis, coding, and creative tasks."
        },
        {
            "content": "Anthropic is an AI safety company founded in 2021, focused on building reliable and interpretable AI systems."
        },
        {
            "content": "LLMs use transformer architecture with attention mechanisms to process text and generate responses."
        }
    ]
    
    # Add documents
    chatbot.add_documents(sample_docs)
    
    # Have a conversation
    questions = [
        "What is Claude?",
        "Who made Claude?",
        "How do LLMs work?"
    ]
    
    for question in questions:
        result = chatbot.ask(question)
        print(f"\nQ: {result['user_query']}")
        print(f"A: {result['assistant_answer']}")
        print(f"Sources used: {result['context_sources']}")
    
    # Save conversation
    chatbot.save_conversation()
    
    # Print statistics
    stats = chatbot.get_statistics()
    print(f"\n=== Conversation Stats ===")
    for key, value in stats.items():
        print(f"{key}: {value}")
```

**Implementation Checklist:**
- [ ] Day 36: Design architecture
- [ ] Day 37: Document ingestion
- [ ] Day 38: Context retrieval
- [ ] Day 39: Answer generation
- [ ] Day 40: Conversation management
- [ ] Day 41: Testing and refinement

**Deliverable:** Production-ready RAG chatbot with full features

---

**Saturday-Sunday (Days 42-43): Testing & Deployment**
**Time:** 3 hours

**Testing Framework:**
```python
import unittest
from datetime import datetime

class TestRAGChatbot(unittest.TestCase):
    def setUp(self):
        """Initialize chatbot for testing"""
        self.chatbot = ProductionRAGChatbot()
        
        # Add test documents
        self.test_docs = [
            {"content": "Paris is the capital of France"},
            {"content": "The Eiffel Tower is in Paris"},
            {"content": "France is in Europe"}
        ]
        self.chatbot.add_documents(self.test_docs)
    
    def test_document_retrieval(self):
        """Test document retrieval"""
        docs = self.chatbot.retrieve_context("Where is Paris?")
        self.assertGreater(len(docs), 0, "Should retrieve documents")
    
    def test_answer_generation(self):
        """Test answer generation"""
        result = self.chatbot.ask("What is Paris?")
        self.assertIn("answer", result or "answer" in result)
        self.assertIsNotNone(result.get("assistant_answer"))
    
    def test_conversation_history(self):
        """Test conversation history"""
        self.chatbot.ask("What is Paris?")
        self.chatbot.ask("What's there?")
        
        # Check history
        self.assertGreaterEqual(len(self.chatbot.conversation_history), 4)
    
    def test_save_conversation(self):
        """Test saving conversation"""
        self.chatbot.ask("Test question")
        filename = self.chatbot.save_conversation()
        
        # Verify file exists
        import os
        self.assertTrue(os.path.exists(filename))
        os.remove(filename)  # Cleanup

if __name__ == "__main__":
    unittest.main()
```

**Deployment Checklist:**
- [ ] All tests passing
- [ ] Error handling working
- [ ] Logging configured
- [ ] Documentation complete
- [ ] GitHub repository updated
- [ ] README with usage examples

**Deliverable:** Tested and documented RAG system

---

## Week 7-8: Refinement & Advanced Features

### Week 7: Enhancement & Evaluation (Days 43-49)

**Monday (Day 43): RAG Evaluation**
**Time:** 2.5 hours

**Metrics:**
```python
class RAGEvaluator:
    def evaluate_retrieval(self, query: str, retrieved_docs: list, relevant_docs: list):
        """Evaluate retrieval quality"""
        # Precision: % of retrieved docs that are relevant
        relevant_retrieved = len([d for d in retrieved_docs if d in relevant_docs])
        precision = relevant_retrieved / max(1, len(retrieved_docs))
        
        # Recall: % of relevant docs that were retrieved
        recall = relevant_retrieved / max(1, len(relevant_docs))
        
        # F1 Score
        f1 = 2 * (precision * recall) / max(0.0001, (precision + recall))
        
        return {
            "precision": precision,
            "recall": recall,
            "f1_score": f1
        }
    
    def evaluate_answer(self, answer: str, reference: str):
        """Evaluate answer quality"""
        # Simple BLEU-like metric
        answer_words = set(answer.lower().split())
        reference_words = set(reference.lower().split())
        
        overlap = len(answer_words & reference_words)
        similarity = overlap / max(1, len(reference_words))
        
        return {"similarity": similarity}
```

---

**Tuesday (Day 44): Performance Optimization**
**Time:** 2.5 hours

**Optimizations:**
```python
class OptimizedRAG:
    def __init__(self):
        self.cache = {}
        self.embedding_cache = {}
    
    def cached_embedding(self, text: str):
        """Cache embeddings"""
        if text not in self.embedding_cache:
            from langchain.embeddings.openai import OpenAIEmbeddings
            embeddings = OpenAIEmbeddings()
            self.embedding_cache[text] = embeddings.embed_query(text)
        
        return self.embedding_cache[text]
    
    def cached_retrieval(self, query: str):
        """Cache retrieval results"""
        if query not in self.cache:
            # Do retrieval
            self.cache[query] = self.retrieve_context(query)
        
        return self.cache[query]
```

---

**Wednesday-Friday (Days 45-48): Advanced Features**
**Time:** 8 hours

**Features to Add:**
1. Multi-turn conversation context
2. Citation tracking
3. Confidence scoring
4. User feedback collection
5. Performance metrics

---

**Saturday-Sunday (Days 49-50): Final Polish**
**Time:** 3 hours

**Final Checklist:**
- [ ] Code cleanup and documentation
- [ ] GitHub repository complete
- [ ] All tests passing
- [ ] Performance metrics collected
- [ ] Demo ready

---

## Project 1: Simple Chatbot (Week 1-2)

### Detailed Implementation

**Project Structure:**
```
project-1-chatbot/
├── README.md
├── requirements.txt
├── chatbot.py
├── examples.py
└── tests/
    └── test_chatbot.py
```

**Step-by-step:**
1. Set up environment
2. Create ChatBot class
3. Implement conversation logic
4. Add error handling
5. Test thoroughly
6. Document with examples

---

## Project 2: RAG Q&A System (Week 5-7)

### Detailed Implementation

**Project Structure:**
```
project-2-rag/
├── README.md
├── requirements.txt
├── config.yaml
├── src/
│   ├── __init__.py
│   ├── document_loader.py
│   ├── embedding_service.py
│   ├── rag_system.py
│   └── api.py
├── examples/
│   ├── sample_documents.txt
│   └── demo.py
└── tests/
    ├── test_loading.py
    ├── test_embedding.py
    └── test_rag.py
```

---

## Project 3: Vector DB Exploration (Week 5-6)

### Hands-on with Different DBs

**Activities:**
1. Test Pinecone
2. Test Weaviate
3. Test Milvus
4. Compare performance
5. Document findings

---

## Project 4: LangChain Application (Week 5-7)

### Complete Application

**Features:**
1. Document ingestion
2. RAG chains
3. Agent loops
4. Tool integration

---

## Resources & Links

### Essential Courses
- DeepLearning.AI: https://www.deeplearning.ai/short-courses/
- Fast.ai: https://course.fast.ai/
- Coursera ML: https://www.coursera.org/

### Key Papers
- Attention: https://arxiv.org/abs/1706.03762
- RAG: https://arxiv.org/abs/2005.11401
- GPT-3: https://arxiv.org/abs/2005.14165

### Tools & Libraries
- LangChain: https://www.langchain.com/
- OpenAI API: https://platform.openai.com/
- Pinecone: https://www.pinecone.io/
- Weaviate: https://weaviate.io/

---

## Progress Tracking

### Week 1-2: Foundations
- [ ] Week 1: Transformers mastered
- [ ] Week 2: Embeddings understood
- [ ] Project 1: Simple chatbot complete

### Week 3-4: Applications
- [ ] Week 3: Prompting techniques
- [ ] Week 4: API applications
- [ ] GitHub repository ready

### Week 5-8: RAG Systems
- [ ] Week 5: RAG foundations
- [ ] Week 6: RAG chatbot complete
- [ ] Week 7-8: Advanced features
- [ ] Final portfolio ready

---

## Success Metrics

**By End of Month 1-2:**
- ✅ 4 working projects
- ✅ 100+ hours of learning
- ✅ GitHub portfolio
- ✅ Production-ready RAG system
- ✅ Confidence to interview for AI roles

---

**Ready to Start?** Begin with Day 1 setup and follow the daily schedule!

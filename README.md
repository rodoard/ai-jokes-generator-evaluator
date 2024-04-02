
# Joke Generator and Evaluator

This project is a web application that allows users to configure joke parameters and generate jokes using an AI model. The application also includes a feature that calls the AI model to evaluate the generated joke and provide an assessment. The user interface consists of two panels side by side: Joke Parameters and Joke Display.

## Prerequisites

To run this project, make sure you have the following installed:

- [SvelteKit](https://kit.svelte.dev/)
- [OpenAI API](https://beta.openai.com/docs/guides/quickstart)
- [Vercel AI SDK](https://vercel.com/docs/ai)

## Getting Started

1. Clone the repository:


```
git clone https://github.com/rodoard/ai-joke-generator-evaluator.git
```

2. Install dependencies:


```
npm install
```

3. Set up environment variables:

Create a .env file in the project root and add the following:


```
OPENAI_API_KEY=your_openai_api_key
```

4. Start the development server:


```
npm run dev
```

5. Access the application at http://localhost:5000

## Joke Generation

Users can configure joke parameters in the Joke Parameters panel. Once the parameters are set, the AI model generates a joke based on the provided configuration.

## Joke Evaluation

After generating a joke, the AI model evaluates the joke and provides an assessment based on the following criteria:

- Humor: The joke's ability to engage the user and make them smile or laugh
- Appropriateness: The suitability of the joke for the intended audience
- Potential offensiveness: The absence of any potential offensiveness or harmful content

## Technologies Used

- SvelteKit
- OpenAI API
- Vercel AI SDK

## Contributing

We welcome contributions from the community. Please submit a pull request if you'd like to contribute.

## License

This project is licensed under the MIT License.

## Additional Information

Much thanks to Encode Club for inspiring this project.

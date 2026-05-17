# gasada-cmd.github.io
Calculus AB George Asada
export default function LHopitalsRuleApp() {
  const practiceProblems = [
    {
      question: "lim(x→0) (sin x)/x",
      answer: "1",
      solution: "Using L'Hopital's Rule: derivative of sin(x) is cos(x), derivative of x is 1. Evaluate cos(0)/1 = 1."
    },
    {
      question: "lim(x→∞) (ln x)/x",
      answer: "0",
      solution: "Apply L'Hopital's Rule: derivative of ln(x) is 1/x, derivative of x is 1. Then lim(x→∞) 1/x = 0."
    },
    {
      question: "lim(x→0) (1 - cos x)/x^2",
      answer: "1/2",
      solution: "Apply L'Hopital twice. First: sin(x)/(2x). Still 0/0. Second: cos(x)/2. Evaluate at x=0 to get 1/2."
    },
    {
      question: "lim(x→∞) x/e^x",
      answer: "0",
      solution: "Apply L'Hopital's Rule: derivative of x is 1, derivative of e^x is e^x. Then lim(x→∞) 1/e^x = 0."
    },
    {
      question: "lim(x→0) (e^x - 1)/x",
      answer: "1",
      solution: "Apply L'Hopital's Rule: derivative of e^x is e^x, derivative of x is 1. Evaluate e^0 = 1."
    }
  ];

  const [answers, setAnswers] = React.useState({});
  const [feedback, setFeedback] = React.useState({});
  const [showSteps, setShowSteps] = React.useState(false);
  const [sliderValue, setSliderValue] = React.useState(1);

  const checkAnswer = (index) => {
    const userAnswer = (answers[index] || "").trim().toLowerCase();
    const correctAnswer = practiceProblems[index].answer.toLowerCase();

    if (userAnswer === correctAnswer) {
      setFeedback({
        ...feedback,
        [index]: {
          correct: true,
          message: "Correct! Great work."
        }
      });
    } else {
      setFeedback({
        ...feedback,
        [index]: {
          correct: false,
          message: `Not quite. Solution: ${practiceProblems[index].solution}`
        }
      });
    }
  };

  return (
    <div className="min-h-screen bg-slate-100 p-6 text-slate-900">
      <div className="max-w-5xl mx-auto bg-white shadow-2xl rounded-3xl p-8 space-y-10">
        <header className="text-center space-y-4">
          <h1 className="text-5xl font-bold">Understanding L'Hopital's Rule</h1>
          <p className="text-xl">Created by George</p>
          <div className="bg-blue-100 rounded-2xl p-4 text-lg">
            <strong>Learning Objective:</strong> After using this app, you should be able to evaluate indeterminate limits using L'Hopital's Rule and justify each step correctly.
          </div>
        </header>

        <section className="space-y-4">
          <h2 className="text-3xl font-semibold">What is L'Hopital's Rule?</h2>
          <p className="text-lg leading-relaxed">
            L'Hopital's Rule is a method used in calculus to evaluate limits that produce indeterminate forms such as
            <span className="font-semibold"> 0/0 </span>
            or
            <span className="font-semibold"> ∞/∞</span>.
          </p>

          <div className="bg-slate-50 border rounded-2xl p-6 text-center text-xl overflow-auto">
            <p>
              If
              <span className="mx-2 font-semibold">lim f(x)/g(x)</span>
              gives an indeterminate form, then:
            </p>
            <div className="mt-4 text-2xl font-bold">
              lim (f(x)/g(x)) = lim (f'(x)/g'(x))
            </div>
            <p className="mt-4 text-base">
              as long as the derivatives exist and the new limit exists.
            </p>
          </div>

          <p className="text-lg leading-relaxed">
            The rule works by differentiating the numerator and denominator separately and then re-evaluating the limit.
          </p>
        </section>

        <section className="space-y-6">
          <h2 className="text-3xl font-semibold">Worked Example 1</h2>

          <div className="bg-green-50 p-6 rounded-2xl border space-y-4">
            <p className="text-xl font-medium">Evaluate:</p>
            <div className="text-2xl font-bold text-center">
              lim(x→0) (sin x)/x
            </div>

            <button
              onClick={() => setShowSteps(!showSteps)}
              className="bg-green-600 text-white px-5 py-3 rounded-xl hover:bg-green-700 transition"
            >
              {showSteps ? "Hide Steps" : "Show Step-by-Step Solution"}
            </button>

            {showSteps && (
              <div className="space-y-3 text-lg">
                <p><strong>Step 1:</strong> Substitute x = 0.</p>
                <p>(sin 0)/0 = 0/0, which is indeterminate.</p>

                <p><strong>Step 2:</strong> Apply L'Hopital's Rule.</p>
                <p>Derivative of sin(x) is cos(x).</p>
                <p>Derivative of x is 1.</p>

                <p><strong>Step 3:</strong> Evaluate the new limit.</p>
                <p>lim(x→0) cos(x)/1 = cos(0) = 1</p>

                <p className="font-bold text-green-700">Final Answer: 1</p>
              </div>
            )}
          </div>
        </section>

        <section className="space-y-6">
          <h2 className="text-3xl font-semibold">Worked Example 2</h2>

          <div className="bg-purple-50 p-6 rounded-2xl border space-y-4">
            <p className="text-xl font-medium">Evaluate:</p>
            <div className="text-2xl font-bold text-center">
              lim(x→∞) (ln x)/x
            </div>

            <div className="space-y-3 text-lg">
              <p><strong>Step 1:</strong> As x approaches infinity, both ln(x) and x approach infinity.</p>
              <p>This creates the indeterminate form ∞/∞.</p>

              <p><strong>Step 2:</strong> Apply L'Hopital's Rule.</p>
              <p>Derivative of ln(x) is 1/x.</p>
              <p>Derivative of x is 1.</p>

              <p><strong>Step 3:</strong> Evaluate the new limit.</p>
              <p>lim(x→∞) 1/x = 0</p>

              <p className="font-bold text-purple-700">Final Answer: 0</p>
            </div>
          </div>
        </section>

        <section className="space-y-6">
          <h2 className="text-3xl font-semibold">Interactive Limit Explorer</h2>

          <div className="bg-orange-50 border rounded-2xl p-6 space-y-6">
            <p className="text-lg">
              Use the slider to explore how the function
              <strong> (e^(ax) - 1)/x </strong>
              changes as the parameter
              <strong> a </strong>
              changes.
            </p>

            <div>
              <label className="block text-lg font-medium mb-2">
                Adjust parameter a: {sliderValue}
              </label>
              <input
                type="range"
                min="1"
                max="10"
                value={sliderValue}
                onChange={(e) => setSliderValue(e.target.value)}
                className="w-full"
              />
            </div>

            <div className="bg-white rounded-xl p-4 text-center text-xl border">
              <p>
                lim(x→0) (e^({sliderValue}x) - 1)/x = {sliderValue}
              </p>
            </div>

            <div className="text-lg leading-relaxed">
              <p>
                By applying L'Hopital's Rule, the derivative of e^({sliderValue}x) is
                {" "}
                {sliderValue}e^({sliderValue}x).
              </p>
              <p>
                Evaluating at x = 0 gives:
                {" "}
                {sliderValue}e^0 = {sliderValue}
              </p>
            </div>
          </div>
        </section>

        <section className="space-y-6">
          <h2 className="text-3xl font-semibold">Practice Problems</h2>

          <div className="space-y-6">
            {practiceProblems.map((problem, index) => (
              <div
                key={index}
                className="bg-slate-50 border rounded-2xl p-6 space-y-4"
              >
                <h3 className="text-xl font-semibold">
                  Problem {index + 1}
                </h3>

                <p className="text-lg font-medium">{problem.question}</p>

                <input
                  type="text"
                  placeholder="Enter your answer"
                  value={answers[index] || ""}
                  onChange={(e) =>
                    setAnswers({
                      ...answers,
                      [index]: e.target.value
                    })
                  }
                  className="w-full border rounded-xl px-4 py-3 text-lg"
                />

                <button
                  onClick={() => checkAnswer(index)}
                  className="bg-blue-600 text-white px-5 py-3 rounded-xl hover:bg-blue-700 transition"
                >
                  Check Answer
                </button>

                {feedback[index] && (
                  <div
                    className={`p-4 rounded-xl text-lg ${
                      feedback[index].correct
                        ? "bg-green-100 text-green-800"
                        : "bg-red-100 text-red-800"
                    }`}
                  >
                    {feedback[index].message}
                  </div>
                )}
              </div>
            ))}
          </div>
        </section>

        <footer className="text-center text-slate-600 text-lg pt-6 border-t">
          <p>
            Keep practicing limits and derivatives to master L'Hopital's Rule.
          </p>
        </footer>
      </div>
    </div>
  );
}

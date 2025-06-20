# gross-close

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Gross-Close | Sales Coaching & Performance Optimization</title>
  <script src="https://cdn.jsdelivr.net/npm/react@18.2.0/umd/react.production.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/react-dom@18.2.0/umd/react-dom.production.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/babel-standalone@7.22.9/babel.min.js"></script>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
</head>
<body>
  <div id="root"></div>
  <script type="text/babel">
    const { useState } = React;

    // Navigation Component
    const Navbar = () => (
      <nav className="bg-gray-800 text-white p-4 sticky top-0 z-10">
        <div className="container mx-auto flex justify-between items-center">
          <h1 className="text-2xl font-bold">Gross-Close</h1>
          <div className="space-x-4">
            <a href="#home" className="hover:text-gray-300">Home</a>
            <a href="#about" className="hover:text-gray-300">About Tom</a>
            <a href="#assessments" className="hover:text-gray-300">Assessments</a>
            <a href="#programs" className="hover:text-gray-300">Programs</a>
            <a href="#contact" className="hover:text-gray-300">Contact</a>
          </div>
        </div>
      </nav>
    );

    // Hero Section
    const Hero = () => (
      <section id="home" className="bg-blue-600 text-white py-20 text-center">
        <div className="container mx-auto px-4">
          <h1 className="text-4xl md:text-5xl font-bold mb-4">Skyrocket Your Sales with Gross-Close</h1>
          <p className="text-xl mb-6">Proven coaching to boost your close rate, commissions, and profitability.</p>
          <a href="#assessments" className="bg-yellow-500 text-black font-bold py-2 px-6 rounded hover:bg-yellow-600">Take the Free Sales IQ Test</a>
        </div>
      </section>
    );

    // About Section
    const About = () => (
      <section id="about" className="py-20 bg-gray-100">
        <div className="container mx-auto px-4">
          <h2 className="text-3xl font-bold text-center mb-8">Meet Tom Grossman</h2>
          <div className="flex flex-col md:flex-row items-center">
            <div className="md:w-1/2 mb-6 md:mb-0">
              <img src="https://via.placeholder.com/400" alt="Tom Grossman" className="rounded-lg shadow-lg mx-auto" />
            </div>
            <div className="md:w-1/2 md:pl-8">
              <p className="text-lg mb-4">With over 25 years in direct sales, <strong>Tom Grossman</strong> is a master at increasing closing percentages and sales probabilities. From upselling in his family’s carpet cleaning business at age 10 to dominating home improvement sales with brands like LeafGuard and Pella, Tom has a proven track record.</p>
              <p className="text-lg mb-4">A former University of Oklahoma wrestler, Tom’s disciplined approach helped him boost his personal closing rate from 25% to over 75%. His coaching delivers measurable results, turning your existing systems into revenue-generating machines.</p>
            </div>
          </div>
        </div>
      </section>
    );

    // Assessment Form Component
    const AssessmentForm = ({ type, questions }) => {
      const [formData, setFormData] = useState({});
      const [submitted, setSubmitted] = useState(false);

      const handleChange = (e, questionId) => {
        setFormData({ ...formData, [questionId]: e.target.value });
      };

      const handleSubmit = (e) => {
        e.preventDefault();
        console.log(`${type} Assessment Data:`, formData); // Simulate sending data to server
        setSubmitted(true);
      };

      return (
        <div className="bg-white p-6 rounded-lg shadow-lg">
          {submitted ? (
            <div className="text-center">
              <h3 className="text-2xl font-bold mb-4">Thank You!</h3>
              <p>We’ve received your {type} assessment. Our team will review your responses and contact you with personalized recommendations.</p>
            </div>
          ) : (
            <form onSubmit={handleSubmit}>
              <h3 className="text-2xl font-bold mb-4">{type} Assessment</h3>
              {questions.map((q, index) => (
                <div key={index} className="mb-4">
                  <label className="block text-lg font-medium mb-2">{q.question}</label>
                  <select
                    className="w-full p-2 border rounded"
                    onChange={(e) => handleChange(e, `q${index + 1}`)}
                    required
                  >
                    <option value="">Select an option</option>
                    {q.options.map((option, i) => (
                      <option key={i} value={option}>{option}</option>
                    ))}
                  </select>
                </div>
              ))}
              <div className="mb-4">
                <label className="block text-lg font-medium mb-2">Name</label>
                <input type="text" className="w-full p-2 border rounded" required />
              </div>
              <div className="mb-4">
                <label className="block text-lg font-medium mb-2">Email</label>
                <input type="email" className="w-full p-2 border rounded" required />
              </div>
              <button type="submit" className="bg-blue-600 text-white font-bold py-2 px-6 rounded hover:bg-blue-700">
                Submit Assessment
              </button>
            </form>
          )}
        </div>
      );
    };

    // Assessments Section
    const Assessments = () => {
      const individualQuestions = [
        { question: "What is your current close rate?", options: ["Below 20%", "20-40%", "40-60%", "Above 60%"] },
        { question: "How confident are you in handling objections?", options: ["Not confident", "Somewhat confident", "Confident", "Very confident"] },
        { question: "How often do you upsell additional products/services?", options: ["Never", "Rarely", "Sometimes", "Always"] },
        { question: "What is your biggest sales challenge?", options: ["Lead generation", "Closing deals", "Handling objections", "Building rapport"] },
        { question: "How many sales calls do you make weekly?", options: ["0-10", "10-20", "20-30", "30+"] },
        { question: "Do you follow a structured sales process?", options: ["No", "Sometimes", "Yes, but inconsistent", "Yes, consistently"] },
        { question: "How do you track your sales performance?", options: ["Not tracked", "Manually", "CRM software", "Other"] },
        { question: "What is your average commission per sale?", options: ["Under $500", "$500-$1000", "$1000-$2000", "Over $2000"] },
        { question: "How often do you receive sales training?", options: ["Never", "Yearly", "Quarterly", "Monthly or more"] },
        { question: "What is your sales goal for the next year?", options: ["Increase close rate", "Higher commissions", "More leads", "All of the above"] },
      ];

      const companyQuestions = [
        { question: "What is your team’s average close rate?", options: ["Below 20%", "20-40%", "40-60%", "Above 60%"] },
        { question: "How standardized is your sales process?", options: ["Not standardized", "Somewhat standardized", "Highly standardized", "Fully optimized"] },
        { question: "What is your team’s biggest weakness?", options: ["Lead generation", "Closing skills", "Team morale", "Training"] },
        { question: "How often do you train your sales team?", options: ["Never", "Yearly", "Quarterly", "Monthly or more"] },
        { question: "What is your annual revenue goal?", options: ["Under $1M", "$1M-$5M", "$5M-$10M", "Over $10M"] },
        { question: "How do you measure sales performance?", options: ["Not measured", "Manual tracking", "CRM", "Advanced analytics"] },
        { question: "What is your lead conversion rate?", options: ["Below 10%", "10-20%", "20-30%", "Above 30%"] },
        { question: "How effective is your team at upselling?", options: ["Not effective", "Somewhat effective", "Effective", "Highly effective"] },
        { question: "Do you have a dedicated sales manager?", options: ["No", "Yes, part-time", "Yes, full-time", "Multiple managers"] },
        { question: "What is your top priority for improvement?", options: ["Close rates", "Profit margins", "Team efficiency", "Lead quality"] },
      ];

      return (
        <section id="assessments" className="py-20">
          <div className="container mx-auto px-4">
            <h2 className="text-3xl font-bold text-center mb-8">Discover Your Sales Potential</h2>
            <p className="text-lg text-center mb-12">Take our free assessments to identify your strengths and areas for growth.</p>
            <div className="grid md:grid-cols-2 gap-8">
              <AssessmentForm type="Sales IQ" questions={individualQuestions} />
              <AssessmentForm type="Company" questions={companyQuestions} />
            </div>
          </div>
        </section>
      );
    };

    // Programs Section
    const Programs = () => (
      <section id="programs" className="py-20 bg-gray-100">
        <div className="container mx-auto px-4">
          <h2 className="text-3xl font-bold text-center mb-8">Our Coaching Programs</h2>
          <div className="grid md:grid-cols-2 gap-8">
            <div className="bg-white p-6 rounded-lg shadow-lg">
              <h3 className="text-2xl font-bold mb-4">Individual Tune-Up</h3>
              <p className="text-lg mb-4">$195 – Immediate action items to boost your sales.</p>
              <p className="mb-4">We analyze your current approach and provide a tailored plan to increase your close rate and commissions.</p>
              <a href="#contact" className="bg-blue-600 text-white font-bold py-2 px-6 rounded hover:bg-blue-700">Get Started</a>
            </div>
            <div className="bg-white p-6 rounded-lg shadow-lg">
              <h3 className="text-2xl font-bold mb-4">Company Tune-Up</h3>
              <p className="text-lg mb-4">$1,995 – Optimize your team’s performance.</p>
              <p className="mb-4">We work with your sales process to deliver strategies that drive immediate profitability.</p>
              <a href="#contact" className="bg-blue-600 text-white font-bold py-2 px-6 rounded hover:bg-blue-700">Get Started</a>
            </div>
            <div className="bg-white p-6 rounded-lg shadow-lg">
              <h3 className="text-2xl font-bold mb-4">Individual Coaching Experience</h3>
              <p className="text-lg mb-4">From $2,500/month – Guaranteed results.</p>
              <p className="mb-4">Personalized coaching to transform your sales performance with Tom’s proven methods.</p>
              <a href="#contact" className="bg-blue-600 text-white font-bold py-2 px-6 rounded hover:bg-blue-700">Get Started</a>
            </div>
            <div className="bg-white p-6 rounded-lg shadow-lg">
              <h3 className="text-2xl font-bold mb-4">Company Coaching Experience</h3>
              <p className="text-lg mb-4">From $25,000 – Transform your business.</p>
              <p className="mb-4">Comprehensive coaching to overhaul your sales team’s performance and profitability.</p>
              <a href="#contact" className="bg-blue-600 text-white font-bold py-2 px-6 rounded hover:bg-blue-700">Get Started</a>
            </div>
          </div>
        </div>
      </section>
    );

    // Contact Section
    const Contact = () => (
      <section id="contact" className="py-20">
        <div className="container mx-auto px-4 text-center">
          <h2 className="text-3xl font-bold mb-8">Get in Touch</h2>
          <p className="text-lg mb-4">Ready to take your sales to the next level? Contact us today!</p>
          <p className="text-lg mb-4">Email: info@gross-close.com | Phone: (555) 123-4567</p>
          <a href="#assessments" className="bg-yellow-500 text-black font-bold py-2 px-6 rounded hover:bg-yellow-600">Take the Free Assessment</a>
        </div>
      </section>
    );

    // Footer
    const Footer = () => (
      <footer className="bg-gray-800 text-white py-6">
        <div className="container mx-auto px-4 text-center">
          <p>&copy; 2025 Gross-Close. All rights reserved.</p>
        </div>
      </footer>
    );

    // Main App Component
    const App = () => (
      <div className="font-roboto">
        <Navbar />
        <Hero />
        <About />
        <Assessments />
        <Programs />
        <Contact />
        <Footer />
      </div>
    );

    // Render the app
    ReactDOM.render(<App />, document.getElementById('root'));
  </script>
</body>
</html>

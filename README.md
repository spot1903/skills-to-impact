# skills-to-impact<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Skills to Impact</title>
    <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        .lucide { width: 1em; height: 1em; }
    </style>
</head>
<body>
    <div id="root"></div>
    
    <script type="text/babel">
        const { useState } = React;
        
        // Lucide icons as components
        const ChevronRight = () => <svg className="lucide" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path d="m9 18 6-6-6-6"/></svg>;
        const ArrowRight = () => <svg className="lucide" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path d="M5 12h14m-7-7 7 7-7 7"/></svg>;
        const Target = () => <svg className="lucide" fill="none" stroke="currentColor" viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><circle cx="12" cy="12" r="6"/><circle cx="12" cy="12" r="2"/></svg>;
        const Cog = () => <svg className="lucide" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path d="M12 20a8 8 0 1 0 0-16 8 8 0 0 0 0 16Z"/><path d="m14.31 8 5.74 9.94M9.69 8h11.48M7.38 12l5.74-9.94M9.69 16 3.95 6.06M14.31 16H2.83m13.79-4-5.74 9.94"/></svg>;
        const Brain = () => <svg className="lucide" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path d="M12 5a3 3 0 1 0-5.997.125 4 4 0 0 0-2.526 5.77 4 4 0 0 0 .556 6.588A4 4 0 1 0 12 18Z"/><path d="M12 5a3 3 0 1 1 5.997.125 4 4 0 0 1 2.526 5.77 4 4 0 0 1-.556 6.588A4 4 0 1 1 12 18Z"/><path d="M15 13a4.5 4.5 0 0 1-3-4 4.5 4.5 0 0 1-3 4"/><path d="M17.599 6.5a3 3 0 0 0 .399-1.375"/><path d="M6.003 5.125A3 3 0 0 0 6.401 6.5"/><path d="M3.477 10.896a4 4 0 0 1 .585-.396"/><path d="M19.938 10.5a4 4 0 0 1 .585.396"/><path d="M6 18a4 4 0 0 1-1.967-.516"/><path d="M19.967 17.484A4 4 0 0 1 18 18"/></svg>;
        const Users = () => <svg className="lucide" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="m22 21-3.5-3.5"/><path d="M16 8v-3a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v3"/></svg>;
        const CheckCircle = () => <svg className="lucide" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/><path d="m9 11 3 3L22 4"/></svg>;

        const SkillsToImpact = () => {
            const [currentView, setCurrentView] = useState('input');
            const [gallupStrengths, setGallupStrengths] = useState('');
            const [inputSkills, setInputSkills] = useState('');
            const [processedResults, setProcessedResults] = useState(null);
            
            const sampleSkills = [
                'Strategic Thinking', 'Project Management', 'Communication', 'Leadership', 'Problem Solving',
                'Data Analysis', 'Financial Modeling', 'Marketing', 'Sales', 'Customer Service',
                'Team Management', 'Business Development', 'Innovation', 'Research', 'Writing',
                'Presentation Skills', 'Negotiation', 'Digital Marketing', 'Social Media', 'Excel',
                'PowerPoint', 'CRM Software', 'Budget Management', 'Risk Assessment', 'Quality Assurance'
            ];

            const processSkillsData = (skillsList) => {
                const processPatterns = {
                    'Problem-Solving Architecture': ['critical thinking', 'problem solving', 'creative problem solving', 'analytical skills', 'decision-making', 'troubleshooting', 'solution'],
                    'Strategic Intelligence': ['strategic thinking', 'strategic planning', 'business strategy', 'planning', 'vision', 'forecasting'],
                    'People & Systems Leadership': ['leadership', 'team leadership', 'management', 'team management', 'supervision', 'mentoring', 'coaching'],
                    'Learning & Innovation Catalyst': ['innovation', 'creativity', 'research', 'learning', 'teaching', 'training', 'development'],
                    'Communication & Influence': ['communication', 'presentation', 'writing', 'public speaking', 'negotiation', 'networking', 'interpersonal']
                };

                const processSkills = {};
                const contentSkills = [];

                skillsList.forEach(skill => {
                    const skillLower = skill.toLowerCase();
                    let categorized = false;

                    Object.entries(processPatterns).forEach(([category, patterns]) => {
                        if (patterns.some(pattern => skillLower.includes(pattern.toLowerCase()))) {
                            if (!processSkills[category]) processSkills[category] = [];
                            processSkills[category].push(skill);
                            categorized = true;
                        }
                    });

                    if (!categorized) {
                        contentSkills.push(skill);
                    }
                });

                const groupedContent = {};
                contentSkills.forEach(skill => {
                    const skillLower = skill.toLowerCase();
                    let category = 'Other Expertise';
                    
                    if (skillLower.includes('financial') || skillLower.includes('finance') || skillLower.includes('accounting') || skillLower.includes('budget')) {
                        category = 'Financial Expertise';
                    } else if (skillLower.includes('marketing') || skillLower.includes('sales') || skillLower.includes('customer') || skillLower.includes('crm')) {
                        category = 'Business & Marketing';
                    } else if (skillLower.includes('software') || skillLower.includes('digital') || skillLower.includes('data') || skillLower.includes('excel') || skillLower.includes('powerpoint')) {
                        category = 'Technology & Tools';
                    } else if (skillLower.includes('project') || skillLower.includes('operations') || skillLower.includes('process') || skillLower.includes('quality')) {
                        category = 'Operations & Project Management';
                    }

                    if (!groupedContent[category]) groupedContent[category] = [];
                    groupedContent[category].push(skill);
                });

                return {
                    processSkills: Object.entries(processSkills).map(([category, skills]) => ({
                        category,
                        skills,
                        impact: getProcessImpact(category)
                    })),
                    contentSkills: Object.entries(groupedContent).map(([category, skills]) => ({
                        category,
                        skills,
                        context: getContentContext(category)
                    }))
                };
            };

            const getProcessImpact = (category) => {
                const impacts = {
                    'Problem-Solving Architecture': 'How you break down complex challenges and build solutions',
                    'Strategic Intelligence': 'How you see patterns, anticipate trends, and plan ahead',
                    'People & Systems Leadership': 'How you align people and processes to achieve results',
                    'Learning & Innovation Catalyst': 'How you generate new ideas and develop others',
                    'Communication & Influence': 'How you connect, persuade, and build relationships'
                };
                return impacts[category] || 'How you apply systematic thinking to create value';
            };

            const getContentContext = (category) => {
                const contexts = {
                    'Financial Expertise': 'Deep technical knowledge in finance and business management',
                    'Business & Marketing': 'Specialized expertise in business operations and customer engagement',
                    'Technology & Tools': 'Technical skills in digital tools and software applications',
                    'Operations & Project Management': 'Expertise in operational efficiency and project execution',
                    'Other Expertise': 'Specialized domain knowledge and technical skills'
                };
                return contexts[category] || 'Specialized domain knowledge and expertise';
            };

            const hrBenefits = [
                {
                    icon: Target,
                    title: "Immediate Role Fit Assessment",
                    description: "See exactly how candidate's approach matches your challenge, regardless of industry background"
                },
                {
                    icon: Brain,
                    title: "Future-Proof Hiring",
                    description: "Process skills transfer across roles and remain valuable as industries evolve"
                },
                {
                    icon: Users,
                    title: "Team Dynamics Prediction", 
                    description: "Understand how this person will work within your existing team structure"
                }
            ];

            return (
                <div className="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-100 p-6">
                    <div className="max-w-4xl mx-auto">
                        
                        <div className="text-center mb-8">
                            <h1 className="text-3xl font-bold text-gray-900 mb-2">Skills to Impact</h1>
                            <p className="text-lg text-gray-600 mb-4">Transform your LinkedIn skills list into the HOW and the WHAT</p>
                            <div className="text-sm text-indigo-700 bg-indigo-50 px-4 py-2 rounded-full inline-block">
                                Showcase your transferable skills alongside domain expertise
                            </div>
                        </div>

                        <div className="flex justify-center mb-8">
                            <div className="flex bg-white rounded-lg p-1 shadow-sm">
                                <button 
                                    onClick={() => setCurrentView('input')}
                                    className={`px-4 py-2 rounded-md transition-colors ${currentView === 'input' ? 'bg-indigo-500 text-white' : 'text-gray-600 hover:text-gray-800'}`}
                                >
                                    Insert Your Skills
                                </button>
                                <button 
                                    onClick={() => setCurrentView('reorganized')}
                                    className={`px-4 py-2 rounded-md transition-colors ${currentView === 'reorganized' ? 'bg-indigo-500 text-white' : 'text-gray-600 hover:text-gray-800'}`}
                                >
                                    The HOW and the WHAT
                                </button>
                                <button 
                                    onClick={() => setCurrentView('hr-view')}
                                    className={`px-4 py-2 rounded-md transition-colors ${currentView === 'hr-view' ? 'bg-indigo-500 text-white' : 'text-gray-600 hover:text-gray-800'}`}
                                >
                                    HR Manager View
                                </button>
                            </div>
                        </div>

                        {currentView === 'input' && (
                            <div className="space-y-6">
                                <div className="bg-white rounded-xl shadow-sm p-6">
                                    <h2 className="text-xl font-bold text-gray-800 mb-4">Insert Your List of Skills as per LinkedIn</h2>
                                    
                                    <div className="mb-4">
                                        <label className="block text-sm font-medium text-gray-700 mb-2">
                                            Copy and paste your skills from LinkedIn (comma-separated)
                                        </label>
                                        <textarea 
                                            placeholder="e.g., Strategic Thinking, Project Management, Communication, Financial Analysis, Leadership, Marketing, Data Analysis..."
                                            className="w-full p-3 border border-gray-300 rounded-lg h-32"
                                            value={inputSkills}
                                            onChange={(e) => setInputSkills(e.target.value)}
                                        />
                                        <p className="text-xs text-gray-500 mt-1">
                                            Tip: Go to your LinkedIn profile → Skills section → copy all your skills
                                        </p>
                                    </div>

                                    <div className="mb-4">
                                        <button 
                                            onClick={() => setInputSkills(sampleSkills.join(', '))}
                                            className="text-sm text-indigo-600 hover:text-indigo-800 underline"
                                        >
                                            Use sample skills to see how it works
                                        </button>
                                    </div>
                                    
                                    <div className="border-t pt-4 mt-6">
                                        <h3 className="font-semibold text-gray-800 mb-2">Add Gallup Strengths (Optional)</h3>
                                        <textarea 
                                            placeholder="e.g., Strategic, Learner, Achiever, Relator, Input..."
                                            className="w-full p-3 border border-gray-300 rounded-lg"
                                            rows="2"
                                            value={gallupStrengths}
                                            onChange={(e) => setGallupStrengths(e.target.value)}
                                        />
                                        <p className="text-xs text-gray-500 mt-1">
                                            If you've taken the CliftonStrengths assessment, add your top 5 strengths
                                        </p>
                                    </div>
                                    
                                    <div className="mt-6 flex justify-center">
                                        <button 
                                            onClick={() => {
                                                if (inputSkills.trim()) {
                                                    const skillsArray = inputSkills.split(',').map(s => s.trim()).filter(s => s);
                                                    setProcessedResults(processSkillsData(skillsArray));
                                                    setCurrentView('reorganized');
                                                }
                                            }}
                                            disabled={!inputSkills.trim()}
                                            className="px-6 py-3 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700 disabled:bg-gray-400 disabled:cursor-not-allowed flex items-center gap-2"
                                        >
                                            Organize My Skills <ArrowRight />
                                        </button>
                                    </div>
                                </div>
                            </div>
                        )}

                        {currentView === 'reorganized' && processedResults && (
                            <div className="space-y-8">
                                
                                <div className="bg-white rounded-xl shadow-sm p-6 border-l-4 border-green-500">
                                    <div className="flex items-center gap-3 mb-4">
                                        <Cog />
                                        <div>
                                            <h2 className="text-xl font-bold text-green-700">HOW You Work (Process Skills - Transferable)</h2>
                                            <p className="text-sm text-gray-600">Your methods and approaches that work across any industry</p>
                                        </div>
                                    </div>
                                    
                                    <div className="space-y-4">
                                        {processedResults.processSkills.map(category => (
                                            <div key={category.category} className="border border-gray-200 rounded-lg p-4">
                                                <h3 className="font-semibold text-gray-800 mb-2">{category.category}</h3>
                                                <div className="flex flex-wrap gap-2 mb-2">
                                                    {category.skills.map(skill => (
                                                        <span key={skill} className="px-2 py-1 bg-green-100 text-green-800 rounded-full text-xs">
                                                            {skill}
                                                        </span>
                                                    ))}
                                                </div>
                                                <p className="text-sm italic text-gray-600">{category.impact}</p>
                                            </div>
                                        ))}
                                    </div>
                                </div>

                                <div className="bg-white rounded-xl shadow-sm p-6 border-l-4 border-blue-500">
                                    <div className="flex items-center gap-3 mb-4">
                                        <Brain />
                                        <div>
                                            <h2 className="text-xl font-bold text-blue-700">WHAT You Know (Content Skills - Domain Specific)</h2>
                                            <p className="text-sm text-gray-600">Your specialized knowledge that gives you credibility</p>
                                        </div>
                                    </div>
                                    
                                    <div className="space-y-4">
                                        {processedResults.contentSkills.map(category => (
                                            <div key={category.category} className="border border-gray-200 rounded-lg p-4">
                                                <h3 className="font-semibold text-gray-800 mb-2">{category.category}</h3>
                                                <div className="flex flex-wrap gap-2 mb-2">
                                                    {category.skills.map(skill => (
                                                        <span key={skill} className="px-2 py-1 bg-blue-100 text-blue-800 rounded-full text-xs">
                                                            {skill}
                                                        </span>
                                                    ))}
                                                </div>
                                                <p className="text-sm italic text-gray-600">{category.context}</p>
                                            </div>
                                        ))}
                                    </div>
                                </div>

                                {gallupStrengths && (
                                    <div className="bg-white rounded-xl shadow-sm p-6 border-l-4 border-purple-500">
                                        <div className="flex items-center gap-3 mb-4">
                                            <Target />
                                            <h2 className="text-xl font-bold text-purple-700">Gallup Strengths Integration</h2>
                                        </div>
                                        <p className="text-sm text-gray-600 mb-3">These natural talents amplify how you apply your process skills:</p>
                                        <div className="flex flex-wrap gap-2">
                                            {gallupStrengths.split(',').map(strength => (
                                                <span key={strength.trim()} className="px-3 py-1 bg-purple-100 text-purple-800 rounded-full text-sm">
                                                    {strength.trim()}
                                                </span>
                                            ))}
                                        </div>
                                    </div>
                                )}
                            </div>
                        )}

                        {currentView === 'hr-view' && (
                            <div className="space-y-6">
                                <div className="bg-white rounded-xl shadow-sm p-6">
                                    <h2 className="text-2xl font-bold text-gray-800 mb-6">Why This Matters for HR & Hiring Managers</h2>
                                    
                                    <div className="grid md:grid-cols-3 gap-6 mb-8">
                                        {hrBenefits.map((benefit, index) => {
                                            const IconComponent = benefit.icon;
                                            return (
                                                <div key={index} className="text-center">
                                                    <IconComponent />
                                                    <h3 className="font-semibold text-gray-800 mb-2 mt-3">{benefit.title}</h3>
                                                    <p className="text-sm text-gray-600">{benefit.description}</p>
                                                </div>
                                            );
                                        })}
                                    </div>

                                    <div className="bg-indigo-50 rounded-lg p-6">
                                        <h3 className="font-semibold text-indigo-900 mb-3">Quick Assessment Framework</h3>
                                        <div className="space-y-3">
                                            <div className="flex items-start gap-3">
                                                <CheckCircle />
                                                <div>
                                                    <p className="font-medium text-gray-800">Process Skills → Role Adaptability</p>
                                                    <p className="text-sm text-gray-600">Can this person solve problems and lead in our context?</p>
                                                </div>
                                            </div>
                                            <div className="flex items-start gap-3">
                                                <CheckCircle />
                                                <div>
                                                    <p className="font-medium text-gray-800">Content Skills → Immediate Contribution</p>
                                                    <p className="text-sm text-gray-600">Do they have the technical knowledge to hit the ground running?</p>
                                                </div>
                                            </div>
                                            <div className="flex items-start gap-3">
                                                <CheckCircle />
                                                <div>
                                                    <p className="font-medium text-gray-800">Strengths → Team Dynamics</p>
                                                    <p className="text-sm text-gray-600">How will their natural patterns complement our team?</p>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>

                                <div className="bg-white rounded-xl shadow-sm p-6">
                                    <h3 className="text-lg font-semibold text-gray-800 mb-4">Traditional vs The HOW and the WHAT Approach</h3>
                                    <div className="grid md:grid-cols-2 gap-6">
                                        <div>
                                            <h4 className="font-medium text-red-700 mb-2">❌ Traditional Skills List Problem</h4>
                                            <ul className="text-sm text-gray-600 space-y-1">
                                                <li>• 50+ skills = cognitive overload</li>
                                                <li>• Hard to assess role fit quickly</li>
                                                <li>• Focus on "what" not "how"</li>
                                                <li>• No insight into working style</li>
                                            </ul>
                                        </div>
                                        <div>
                                            <h4 className="font-medium text-green-700 mb-2">✅ The HOW and the WHAT Benefits</h4>
                                            <ul className="text-sm text-gray-600 space-y-1">
                                                <li>• Clear process vs content separation</li>
                                                <li>• Fast assessment of adaptability</li>
                                                <li>• Shows how they think and work</li>
                                                <li>• Predicts team contribution style</li>
                                            </ul>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        )}

                        <div className="mt-8 text-center text-gray-500 text-sm">
                            <p>Skills to Impact - Showcase your transferable skills and domain expertise</p>
                        </div>
                    </div>
                </div>
            );
        };

        ReactDOM.render(<SkillsToImpact />, document.getElementById('root'));
    </script>
</body>
</html>

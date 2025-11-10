import React, { useState, useEffect } from 'react';
import { LineChart, Line, XAxis, YAxis, CartesianGrid, Tooltip, Legend, ResponsiveContainer, BarChart, Bar } from 'recharts';

const BankEvolutionSystem = () => {
  const [activeTab, setActiveTab] = useState('evolve');
  const [numGenerations, setNumGenerations] = useState(100);
  const [mutationRate, setMutationRate] = useState(0.03);
  const [maxPopulation, setMaxPopulation] = useState(120);
  const [isRunning, setIsRunning] = useState(false);
  const [populationHistory, setPopulationHistory] = useState([]);
  const [speciesStats, setSpeciesStats] = useState([]);
  const [savedSpecies, setSavedSpecies] = useState([]);
  const [selectedForSave, setSelectedForSave] = useState(new Set());
  const [selectedForCompete, setSelectedForCompete] = useState(new Set());
  const [numGames, setNumGames] = useState(1000);
  const [competeResults, setCompeteResults] = useState(null);

  useEffect(() => {
    const saved = localStorage.getItem('bankSpecies');
    if (saved) {
      setSavedSpecies(JSON.parse(saved));
    }
  }, []);

  const rollDice = () => {
    return [Math.floor(Math.random() * 6) + 1, Math.floor(Math.random() * 6) + 1];
  };

  const normalizeWeights = (weights) => {
    const sum = weights.placement + weights.rollCount + weights.double + weights.total;
    return {
      placement: weights.placement / sum,
      rollCount: weights.rollCount / sum,
      double: weights.double / sum,
      total: weights.total / sum
    };
  };

  const createStrategy = (genome) => {
    return (turnTotal, rollCount, currentScore, otherScores, justDoubled) => {
      if (rollCount <= 3) return false;
      
      let bankScore = 0;
      
      const potentialScore = currentScore + turnTotal;
      const maxOtherScore = Math.max(...otherScores);
      const minOtherScore = Math.min(...otherScores);
      let placementScore = 0;
      if (potentialScore > maxOtherScore) placementScore = 100;
      else if (potentialScore > minOtherScore) placementScore = 50;
      bankScore += placementScore * genome.weights.placement;
      
      const rollScore = Math.min(100, (rollCount - 3) * 10);
      bankScore += rollScore * genome.weights.rollCount;
      
      const doubleScore = justDoubled ? 100 : 0;
      bankScore += doubleScore * genome.weights.double;
      
      const totalScore = Math.min(100, (turnTotal / 200) * 100);
      bankScore += totalScore * genome.weights.total;
      
      return bankScore >= genome.threshold;
    };
  };

  const createInitialGenome = () => {
    return {
      weights: { placement: 0.25, rollCount: 0.25, double: 0.25, total: 0.25 },
      threshold: 50,
      species: 'Origin',
      speciesId: 0,
      generation: 0
    };
  };

  const mutateGenome = (parentGenome, generation, newSpeciesId) => {
    const newWeights = { ...parentGenome.weights };
    
    Object.keys(newWeights).forEach(key => {
      const adjustment = (Math.random() * 0.1 - 0.05);
      newWeights[key] = Math.max(0.01, newWeights[key] + adjustment);
    });
    
    return {
      weights: normalizeWeights(newWeights),
      threshold: Math.max(10, Math.min(90, parentGenome.threshold + (Math.random() * 20 - 10))),
      species: 'Species_' + newSpeciesId,
      speciesId: newSpeciesId,
      generation: generation
    };
  };

  const generateColor = (id) => {
    const hue = (id * 137.508) % 360;
    return 'hsl(' + hue + ', 70%, 50%)';
  };

  const playRound = (strategy, currentScore, otherScores) => {
    let turnTotal = 0;
    let rollCount = 0;
    let justDoubled = false;

    while (true) {
      rollCount++;
      const dice = rollDice();
      const die1 = dice[0];
      const die2 = dice[1];
      const sum = die1 + die2;
      const isDoubles = die1 === die2;

      if (rollCount <= 3) {
        if (sum === 7) {
          turnTotal += 70;
        } else {
          turnTotal += sum;
        }
        justDoubled = false;
      } else {
        if (sum === 7) {
          return 0;
        }
        
        if (isDoubles) {
          turnTotal = turnTotal * 2;
          justDoubled = true;
        } else {
          turnTotal += sum;
          justDoubled = false;
        }
      }

      if (strategy(turnTotal, rollCount, currentScore, otherScores, justDoubled)) {
        return turnTotal;
      }
    }
  };

  const playGame = (players) => {
    const scores = {};
    players.forEach(p => {
      scores[p.id] = 0;
    });

    for (let round = 0; round < 10; round++) {
      for (const player of players) {
        const otherScores = players
          .filter(p => p.id !== player.id)
          .map(p => scores[p.id]);
        
        const strategy = createStrategy(player.genome);
        const roundScore = playRound(strategy, scores[player.id], otherScores);
        
        scores[player.id] += roundScore;
      }
    }

    return scores;
  };

  const runEvolution = () => {
    setIsRunning(true);
    
    setTimeout(() => {
      let population = [];
      let idCounter = 0;
      let speciesCounter = 1;
      
      const originGenome = createInitialGenome();
      for (let i = 0; i < maxPopulation; i++) {
        population.push({ id: idCounter++, genome: { ...originGenome } });
      }

      const history = [];
      const speciesTracker = {};
      const speciesColors = { 0: '#8b5cf6' };
      
      speciesTracker[0] = { maxPop: maxPopulation, genome: originGenome, name: 'Origin' };
      
      const countBySpeciesId = (pop) => {
        const counts = {};
        pop.forEach(p => {
          const sid = p.genome.speciesId;
          counts[sid] = (counts[sid] || 0) + 1;
        });
        return counts;
      };
      
      const initialCounts = countBySpeciesId(population);
      history.push({ generation: 0, ...initialCounts });

      for (let gen = 1; gen <= numGenerations; gen++) {
        if (population.length === 0) break;
        
        for (let game = 0; game < 20; game++) {
          if (population.length < 4) break;
          
          const shuffled = [...population].sort(() => Math.random() - 0.5);
          const selectedPlayers = shuffled.slice(0, 4);
          
          const scores = playGame(selectedPlayers);
          
          const sortedPlayers = selectedPlayers.sort((a, b) => scores[b.id] - scores[a.id]);
          const winner = sortedPlayers[0];
          const losers = sortedPlayers.slice(1);
          
          if (population.length < maxPopulation) {
            let childGenome;
            
            if (Math.random() < mutationRate) {
              const newSpeciesId = speciesCounter++;
              childGenome = mutateGenome(winner.genome, gen, newSpeciesId);
              
              speciesTracker[newSpeciesId] = {
                maxPop: 1,
                genome: childGenome,
                name: childGenome.species
              };
              speciesColors[newSpeciesId] = generateColor(newSpeciesId);
            } else {
              childGenome = { ...winner.genome };
            }
            
            population.push({ id: idCounter++, genome: childGenome });
          }
          
          losers.forEach(loser => {
            if (Math.random() < 0.25) {
              const index = population.findIndex(p => p.id === loser.id);
              if (index !== -1) {
                population.splice(index, 1);
              }
            }
          });
        }
        
        const currentCounts = countBySpeciesId(population);
        Object.keys(currentCounts).forEach(sid => {
          if (speciesTracker[sid]) {
            speciesTracker[sid].maxPop = Math.max(
              speciesTracker[sid].maxPop, 
              currentCounts[sid]
            );
          }
        });
        
        history.push({ generation: gen, ...currentCounts });
      }

      setPopulationHistory(history);
      
      const sortedSpecies = Object.entries(speciesTracker)
        .map(([id, data]) => {
          return {
            id: parseInt(id),
            name: data.name,
            maxPop: data.maxPop,
            weights: data.genome.weights,
            threshold: data.genome.threshold,
            color: speciesColors[id],
            genome: data.genome
          };
        })
        .sort((a, b) => b.maxPop - a.maxPop);
      
      setSpeciesStats(sortedSpecies);
      setSelectedForSave(new Set());
      setIsRunning(false);
    }, 100);
  };

  const toggleSaveSelection = (speciesId) => {
    const newSet = new Set(selectedForSave);
    if (newSet.has(speciesId)) {
      newSet.delete(speciesId);
    } else {
      newSet.add(speciesId);
    }
    setSelectedForSave(newSet);
  };

  const saveSelectedSpecies = () => {
    const toSave = speciesStats.filter(s => selectedForSave.has(s.id));
    const newSaved = [...savedSpecies];
    
    toSave.forEach(species => {
      if (!newSaved.find(s => s.name === species.name)) {
        newSaved.push(species);
      }
    });
    
    setSavedSpecies(newSaved);
    localStorage.setItem('bankSpecies', JSON.stringify(newSaved));
    setSelectedForSave(new Set());
    alert('Species saved successfully!');
  };

  const removeSavedSpecies = (name) => {
    const newSaved = savedSpecies.filter(s => s.name !== name);
    setSavedSpecies(newSaved);
    localStorage.setItem('bankSpecies', JSON.stringify(newSaved));
  };

  const toggleCompeteSelection = (name) => {
    const newSet = new Set(selectedForCompete);
    if (newSet.has(name)) {
      newSet.delete(name);
    } else {
      newSet.add(name);
    }
    setSelectedForCompete(newSet);
  };

  const runCompetition = () => {
    if (selectedForCompete.size < 2) {
      alert('Please select at least 2 species to compete');
      return;
    }

    setIsRunning(true);

    setTimeout(() => {
      const competingSpecies = savedSpecies.filter(s => selectedForCompete.has(s.name));
      const results = {};
      
      competingSpecies.forEach(species => {
        results[species.name] = { wins: 0, totalScore: 0, species: species };
      });

      for (let i = 0; i < numGames; i++) {
        const players = competingSpecies.map((species, idx) => ({
          id: idx,
          genome: species.genome,
          name: species.name
        }));

        const scores = playGame(players);
        const maxScore = Math.max(...Object.values(scores));
        
        players.forEach(p => {
          results[p.name].totalScore += scores[p.id];
          if (scores[p.id] === maxScore) {
            results[p.name].wins++;
          }
        });
      }

      const sortedResults = Object.values(results)
        .map(r => ({
          name: r.species.name,
          wins: r.wins,
          winRate: (r.wins / numGames * 100).toFixed(1),
          avgScore: (r.totalScore / numGames).toFixed(1),
          color: r.species.color
        }))
        .sort((a, b) => b.wins - a.wins);

      setCompeteResults(sortedResults);
      setIsRunning(false);
    }, 100);
  };

  const calculateGoodSpecies = () => {
    const top10 = speciesStats.slice(0, 10);
    if (top10.length === 0) return null;
    
    const avgWeights = {
      placement: top10.reduce((sum, s) => sum + s.weights.placement, 0) / top10.length,
      rollCount: top10.reduce((sum, s) => sum + s.weights.rollCount, 0) / top10.length,
      double: top10.reduce((sum, s) => sum + s.weights.double, 0) / top10.length,
      total: top10.reduce((sum, s) => sum + s.weights.total, 0) / top10.length
    };
    const avgThreshold = top10.reduce((sum, s) => sum + s.threshold, 0) / top10.length;
    
    return { avgWeights, avgThreshold };
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-green-50 to-blue-100 p-8">
      <div className="max-w-7xl mx-auto">
        <header className="text-center mb-8">
          <h1 className="text-4xl font-bold text-green-900 mb-2">
            🧬 BANK Game Evolution System
          </h1>
          <p className="text-gray-600 text-lg">
            Evolve and compete strategies through natural selection
          </p>
        </header>
        
        <div className="flex gap-3 mb-8 bg-white p-3 rounded-lg shadow-lg">
          <button
            onClick={() => setActiveTab('evolve')}
            className={'flex-1 py-3 px-6 rounded-lg font-semibold transition ' + (activeTab === 'evolve' ? 'bg-green-600 text-white' : 'bg-gray-100 text-gray-700 hover:bg-gray-200')}
          >
            Evolve
          </button>
          <button
            onClick={() => setActiveTab('compete')}
            className={'flex-1 py-3 px-6 rounded-lg font-semibold transition ' + (activeTab === 'compete' ? 'bg-green-600 text-white' : 'bg-gray-100 text-gray-700 hover:bg-gray-200')}
          >
            Compete
          </button>
          <button
            onClick={() => setActiveTab('saved')}
            className={'flex-1 py-3 px-6 rounded-lg font-semibold transition ' + (activeTab === 'saved' ? 'bg-green-600 text-white' : 'bg-gray-100 text-gray-700 hover:bg-gray-200')}
          >
            Saved Species ({savedSpecies.length})
          </button>
        </div>

        {activeTab === 'evolve' && (
          <div>
            <div className="bg-white rounded-lg shadow-lg p-6 mb-6">
              <h2 className="text-2xl font-bold text-gray-800 mb-4">Simulation Settings</h2>
              <div className="grid grid-cols-1 md:grid-cols-3 gap-4 mb-4">
                <div>
                  <label className="block text-sm font-semibold text-gray-700 mb-1">
                    Number of Generations:
                  </label>
                  <input
                    type="number"
                    value={numGenerations}
                    onChange={(e) => setNumGenerations(Math.max(1, parseInt(e.target.value) || 1))}
                    className="w-full border-2 border-green-300 rounded px-4 py-2 text-lg"
                    min="1"
                  />
                </div>
                <div>
                  <label className="block text-sm font-semibold text-gray-700 mb-1">
                    Mutation Rate:
                  </label>
                  <input
                    type="number"
                    step="0.01"
                    value={mutationRate}
                    onChange={(e) => setMutationRate(Math.max(0, Math.min(1, parseFloat(e.target.value) || 0)))}
                    className="w-full border-2 border-purple-300 rounded px-4 py-2 text-lg"
                    min="0"
                    max="1"
                  />
                </div>
                <div>
                  <label className="block text-sm font-semibold text-gray-700 mb-1">
                    Max Population:
                  </label>
                  <input
                    type="number"
                    value={maxPopulation}
                    onChange={(e) => setMaxPopulation(Math.max(10, parseInt(e.target.value) || 120))}
                    className="w-full border-2 border-blue-300 rounded px-4 py-2 text-lg"
                    min="10"
                  />
                </div>
              </div>
              <button
                onClick={runEvolution}
                disabled={isRunning}
                className="bg-green-600 hover:bg-green-700 disabled:bg-gray-400 text-white font-bold py-3 px-8 rounded-lg transition"
              >
                {isRunning ? 'Running...' : 'Start Evolution'}
              </button>

              <div className="bg-blue-50 p-4 rounded-lg border-2 border-blue-200 mt-6">
                <h3 className="font-bold text-blue-900 mb-2">Evolution Rules</h3>
                <ul className="text-sm text-gray-700 space-y-1 ml-5 list-disc">
                  <li>Population starts with {maxPopulation} individuals of the Origin species</li>
                  <li>Origin species values all 4 factors equally (25% each)</li>
                  <li>Each generation: 20 random 4-player games</li>
                  <li>Winner breeds (creates offspring) if pop &lt; {maxPopulation}</li>
                  <li>Mutation rate: {(mutationRate * 100).toFixed(0)}% chance offspring becomes new species</li>
                  <li>Mutations adjust each weight by ±5%, then normalize to 100%</li>
                  <li>Bottom 3 players each have 25% chance of elimination</li>
                </ul>
              </div>

              <div className="bg-purple-50 p-4 rounded-lg border-2 border-purple-200 mt-4">
                <h3 className="font-bold text-purple-900 mb-2">Strategy Factors (Always sum to 100%)</h3>
                <ul className="text-sm text-gray-700 space-y-1 ml-5 list-disc">
                  <li><strong>Placement:</strong> Being in 1st place after banking</li>
                  <li><strong>Roll Count:</strong> Risk from rolling many times</li>
                  <li><strong>Double:</strong> Banking right after rolling doubles</li>
                  <li><strong>Total:</strong> Current turn total score</li>
                </ul>
              </div>

              <div className="bg-amber-50 p-4 rounded-lg border-2 border-amber-200 mt-4">
                <h3 className="font-bold text-amber-900 mb-2">What is "Threshold"?</h3>
                <p className="text-sm text-gray-700">
                  The threshold is the minimum banking score needed for a player to bank. Each factor (placement, roll count, double, total) contributes to a banking score between 0-100. When this combined score reaches the threshold, the player banks. A lower threshold means banking more aggressively, while a higher threshold means taking more risks for bigger scores.
                </p>
              </div>
            </div>

            {populationHistory.length > 0 && (
              <>
                <div className="bg-white rounded-lg shadow-lg p-6 mb-6">
                  <h2 className="text-2xl font-bold text-gray-800 mb-4">Population Over Time (Top 10 Species)</h2>
                  <ResponsiveContainer width="100%" height={500}>
                    <LineChart data={populationHistory}>
                      <CartesianGrid strokeDasharray="3 3" />
                      <XAxis dataKey="generation" label={{ value: 'Generation', position: 'insideBottom', offset: -5 }} />
                      <YAxis label={{ value: 'Population', angle: -90, position: 'insideLeft' }} />
                      <Tooltip />
                      <Legend />
                      {speciesStats.slice(0, 10).map(species => (
                        <Line
                          key={species.id}
                          type="monotone"
                          dataKey={species.id.toString()}
                          name={species.name}
                          stroke={species.color}
                          strokeWidth={species.id === 0 ? 3 : 2}
                          dot={false}
                        />
                      ))}
                    </LineChart>
                  </ResponsiveContainer>
                </div>

                {calculateGoodSpecies() && (
                  <div className="bg-gradient-to-r from-yellow-50 to-amber-50 rounded-lg shadow-lg p-6 mb-6 border-2 border-yellow-300">
                    <h2 className="text-2xl font-bold text-amber-900 mb-4">
                      ⭐ "Good Species" - Average of Top 10
                    </h2>
                    {(() => {
                      const good = calculateGoodSpecies();
                      return (
                        <div className="grid grid-cols-2 md:grid-cols-5 gap-4">
                          <div className="bg-white p-4 rounded-lg border-2 border-purple-300 text-center">
                            <p className="text-sm text-gray-600 mb-1">Placement</p>
                            <p className="text-2xl font-bold text-purple-700">{(good.avgWeights.placement * 100).toFixed(1)}%</p>
                          </div>
                          <div className="bg-white p-4 rounded-lg border-2 border-blue-300 text-center">
                            <p className="text-sm text-gray-600 mb-1">Roll Count</p>
                            <p className="text-2xl font-bold text-blue-700">{(good.avgWeights.rollCount * 100).toFixed(1)}%</p>
                          </div>
                          <div className="bg-white p-4 rounded-lg border-2 border-green-300 text-center">
                            <p className="text-sm text-gray-600 mb-1">Double</p>
                            <p className="text-2xl font-bold text-green-700">{(good.avgWeights.double * 100).toFixed(1)}%</p>
                          </div>
                          <div className="bg-white p-4 rounded-lg border-2 border-orange-300 text-center">
                            <p className="text-sm text-gray-600 mb-1">Total</p>
                            <p className="text-2xl font-bold text-orange-700">{(good.avgWeights.total * 100).toFixed(1)}%</p>
                          </div>
                          <div className="bg-white p-4 rounded-lg border-2 border-amber-300 text-center">
                            <p className="text-sm text-gray-600 mb-1">Threshold</p>
                            <p className="text-2xl font-bold text-amber-700">{good.avgThreshold.toFixed(0)}</p>
                          </div>
                        </div>
                      );
                    })()}
                  </div>
                )}

                <div className="bg-white rounded-lg shadow-lg p-6">
                  <h2 className="text-2xl font-bold text-gray-800 mb-2">Top 20 Species Rankings</h2>
                  <p className="text-gray-600 mb-4">Select species to save for competition</p>
                  <div className="overflow-x-auto">
                    <table className="w-full text-sm">
                      <thead className="bg-gray-100">
                        <tr>
                          <th className="p-2 text-left">Save</th>
                          <th className="p-2 text-left">Rank</th>
                          <th className="p-2 text-left">Species</th>
                          <th className="p-2 text-right">Max Pop</th>
                          <th className="p-2 text-right">Placement</th>
                          <th className="p-2 text-right">Roll Count</th>
                          <th className="p-2 text-right">Double</th>
                          <th className="p-2 text-right">Total</th>
                          <th className="p-2 text-right">Threshold</th>
                        </tr>
                      </thead>
                      <tbody>
                        {speciesStats.slice(0, 20).map((species, idx) => (
                          <tr key={species.id} className="border-b hover:bg-gray-50">
                            <td className="p-2">
                              <input
                                type="checkbox"
                                checked={selectedForSave.has(species.id)}
                                onChange={() => toggleSaveSelection(species.id)}
                                className="w-5 h-5 cursor-pointer"
                              />
                            </td>
                            <td className="p-2 font-semibold">{idx + 1}</td>
                            <td className="p-2">
                              <span
                                className="inline-block w-3 h-3 rounded-full mr-2"
                                style={{ backgroundColor: species.color }}
                              />
                              {species.name}
                            </td>
                            <td className="p-2 text-right font-bold">{species.maxPop}</td>
                            <td className="p-2 text-right">{(species.weights.placement * 100).toFixed(1)}%</td>
                            <td className="p-2 text-right">{(species.weights.rollCount * 100).toFixed(1)}%</td>
                            <td className="p-2 text-right">{(species.weights.double * 100).toFixed(1)}%</td>
                            <td className="p-2 text-right">{(species.weights.total * 100).toFixed(1)}%</td>
                            <td className="p-2 text-right">{species.threshold.toFixed(0)}</td>
                          </tr>
                        ))}
                      </tbody>
                    </table>
                  </div>
                  <button
                    onClick={saveSelectedSpecies}
                    disabled={selectedForSave.size === 0}
                    className="mt-4 bg-green-600 hover:bg-green-700 disabled:bg-gray-400 text-white font-bold py-2 px-6 rounded-lg transition"
                  >
                    Save Selected Species ({selectedForSave.size})
                  </button>
                  <p className="text-sm text-gray-600 mt-4 text-center">
                    Showing top 20 of {speciesStats.length} total unique species created
                  </p>
                </div>
              </>
            )}
          </div>
        )}

        {activeTab === 'compete' && (
          <div>
            <div className="bg-white rounded-lg shadow-lg p-6 mb-6">
              <h2 className="text-2xl font-bold text-gray-800 mb-4">Competition Settings</h2>
              <div className="mb-4">
                <label className="block text-sm font-semibold text-gray-700 mb-1">
                  Number of Games:
                </label>
                <input
                  type="number"
                  value={numGames}
                  onChange={(e) => setNumGames(Math.max(1, parseInt(e.target.value) || 1000))}
                  className="w-64 border-2 border-green-300 rounded px-4 py-2 text-lg"
                  min="1"
                />
              </div>

              <h3 className="text-lg font-semibold text-gray-800 mt-6 mb-3">
                Select Species to Compete (choose at least 2)
              </h3>
              
              {savedSpecies.length === 0 ? (
                <p className="text-gray-600">No saved species yet. Run an evolution and save some species first!</p>
              ) : (
                <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-3">
                  {savedSpecies.map(species => (
                    <label key={species.name} className="flex items-center gap-3 p-3 border-2 border-gray-200 rounded-lg hover:bg-gray-50 cursor-pointer">
                      <input
                        type="checkbox"
                        checked={selectedForCompete.has(species.name)}
                        onChange={() => toggleCompeteSelection(species.name)}
                        className="w-5 h-5"
                      />
                      <span
                        className="w-4 h-4 rounded-full"
                        style={{ backgroundColor: species.color }}
                      />
                      <span className="font-medium">{species.name}</span>
                    </label>
                  ))}
                </div>
              )}

              <button
                onClick={runCompetition}
                disabled={isRunning || selectedForCompete.size < 2}
                className="mt-6 bg-green-600 hover:bg-green-700 disabled:bg-gray-400 text-white font-bold py-3 px-8 rounded-lg transition"
              >
                {isRunning ? 'Running...' : 'Start Competition'}
              </button>
            </div>

            {competeResults && (
              <>
                <div className="bg-white rounded-lg shadow-lg p-6 mb-6">
                  <h2 className="text-2xl font-bold text-gray-800 mb-4">Competition Results</h2>
                  <ResponsiveContainer width="100%" height={400}>
                    <BarChart data={competeResults}>
                      <CartesianGrid strokeDasharray="3 3" />
                      <XAxis dataKey="name" />
                      <YAxis />
                      <Tooltip />
                      <Legend />
                      <Bar dataKey="wins" fill="#22c55e" name="Wins" />
                    </BarChart>
                  </ResponsiveContainer>
                </div>

                <div className="bg-white rounded-lg shadow-lg p-6">
                  <h2 className="text-2xl font-bold text-gray-800 mb-4">Detailed Results</h2>
                  <div className="overflow-x-auto">
                    <table className="w-full">
                      <thead className="bg-gray-100">
                        <tr>
                          <th className="p-3 text-left">Rank</th>
                          <th className="p-3 text-left">Species</th>
                          <th className="p-3 text-right">Wins</th>
                          <th className="p-3 text-right">Win Rate</th>
                          <th className="p-3 text-right">Avg Score</th>
                        </tr>
                      </thead>
                      <tbody>
                        {competeResults.map((result, idx) => (
                          <tr key={result.name} className="border-b hover:bg-gray-50">
                            <td className="p-3 font-semibold">{idx + 1}</td>
                            <td className="p-3">
                              <span
                                className="inline-block w-3 h-3 rounded-full mr-2"
                                style={{ backgroundColor: result.color }}
                              />
                              {result.name}
                            </td>
                            <td className="p-3 text-right font-bold">{result.wins}</td>
                            <td className="p-3 text-right">{result.winRate}%</td>
                            <td className="p-3 text-right">{result.avgScore}</td>
                          </tr>
                        ))}
                      </tbody>
                    </table>
                  </div>
                </div>
              </>
            )}
          </div>
        )}

        {activeTab === 'saved' && (
          <div className="bg-white rounded-lg shadow-lg p-6">
            <h2 className="text-2xl font-bold text-gray-800 mb-4">
              Saved Species ({savedSpecies.length})
            </h2>
            
            {savedSpecies.length === 0 ? (
              <p className="text-gray-600">No saved species yet. Run an evolution and save some species!</p>
            ) : (
              <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
                {savedSpecies.map(species => (
                  <div key={species.name} className="border-2 border-gray-200 rounded-lg p-4 relative">
                    <button
                      onClick={() => removeSavedSpecies(species.name)}
                      className="absolute top-2 right-2 bg-red-500 hover:bg-red-600 text-white px-2 py-1 rounded text-sm"
                    >
                      Remove
                    </button>
                    
                    <div className="flex items-center gap-2 mb-3">
                      <span
                        className="w-4 h-4 rounded-full"
                        style={{ backgroundColor: species.color }}
                      />
                      <h3 className="font-bold text-lg">{species.name}</h3>
                    </div>
                    
                    <div className="text-sm space-y-1">
                      <p><strong>Max Pop:</strong> {species.maxPop}</p>
                      <p><strong>Placement:</strong> {(species.weights.placement * 100).toFixed(1)}%</p>
                      <p><strong>Roll Count:</strong> {(species.weights.rollCount * 100).toFixed(1)}%</p>
                      <p><strong>Double:</strong> {(species.weights.double * 100).toFixed(1)}%</p>
                      <p><strong>Total:</strong> {(species.weights.total * 100).toFixed(1)}%</p>
                      <p><strong>Threshold:</strong> {species.threshold.toFixed(0)}</p>
                    </div>
                  </div>
                ))}
              </div>
            )}
          </div>
        )}
      </div>
    </div>
  );
};

export default BankEvolutionSystem;

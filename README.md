import { useState, useEffect } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { Textarea } from "@/components/ui/textarea";

const mockPredictions = [
  {
    id: 1,
    match: "Real Madrid vs Barcelona",
    prediction: "Победа Real Madrid",
    status: "live"
  },
  {
    id: 2,
    match: "Man City vs Arsenal",
    prediction: "Тотал больше 2.5",
    status: "pending"
  }
];

export default function LivePredictions() {
  const [predictions, setPredictions] = useState(mockPredictions);
  const [match, setMatch] = useState("");
  const [prediction, setPrediction] = useState("");

  const addPrediction = () => {
    if (!match || !prediction) return;
    const newPrediction = {
      id: Date.now(),
      match,
      prediction,
      status: "pending"
    };
    setPredictions([newPrediction, ...predictions]);
    setMatch("");
    setPrediction("");
  };

  return (
    <div className="p-4 max-w-3xl mx-auto space-y-4">
      <h1 className="text-2xl font-bold">Прогнозы на спорт (LIVE)</h1>

      <div className="bg-gray-100 p-4 rounded-xl shadow">
        <h2 className="text-lg font-semibold mb-2">Добавить прогноз</h2>
        <Input
          placeholder="Матч (например: PSG vs Bayern)"
          value={match}
          onChange={(e) => setMatch(e.target.value)}
          className="mb-2"
        />
        <Textarea
          placeholder="Ваш прогноз"
          value={prediction}
          onChange={(e) => setPrediction(e.target.value)}
          className="mb-2"
        />
        <Button onClick={addPrediction}>Добавить</Button>
      </div>

      <div className="grid gap-4">
        {predictions.map((p) => (
          <Card key={p.id} className="border-l-4 border-blue-500">
            <CardContent className="p-4">
              <h3 className="text-lg font-bold">{p.match}</h3>
              <p>{p.prediction}</p>
              <span className="text-sm text-gray-500">Статус: {p.status}</span>
            </CardContent>
          </Card>
        ))}
      </div>
    </div>
  );
}

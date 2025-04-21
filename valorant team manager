import React, { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { GripVertical, Trophy } from "lucide-react";
import { motion } from "framer-motion";

const initialMembers = [
  { name: "Alice", rank: 3, wins: 0 },
  { name: "Bob", rank: 2, wins: 0 },
  { name: "Charlie", rank: 1, wins: 0 },
  { name: "David", rank: 2, wins: 0 },
  { name: "Eve", rank: 3, wins: 0 },
  { name: "Frank", rank: 1, wins: 0 }
];

export default function ValorantTeamManager() {
  const [members, setMembers] = useState(initialMembers);
  const [teamA, setTeamA] = useState([]);
  const [teamB, setTeamB] = useState([]);

  const shuffleTeams = () => {
    const shuffled = [...members].sort(() => Math.random() - 0.5);
    const sorted = shuffled.sort((a, b) => b.rank - a.rank);
    const a = [], b = [], total = [0, 0];
    sorted.forEach((member) => {
      const team = total[0] <= total[1] ? a : b;
      const sum = total[0] <= total[1] ? 0 : 1;
      team.push(member);
      total[sum] += member.rank;
    });
    setTeamA(a);
    setTeamB(b);
  };

  const handleWin = (team) => {
    const updated = members.map((m) => {
      const isWinner = (team === 'A' ? teamA : teamB).some(t => t.name === m.name);
      return isWinner ? { ...m, wins: m.wins + 1 } : m;
    });
    setMembers(updated);
  };

  return (
    <div className="grid grid-cols-3 gap-4 p-4">
      <div>
        <h2 className="text-xl font-bold mb-2">メンバー一覧</h2>
        {members.map((m) => (
          <Card key={m.name} className="mb-2 p-2 flex items-center justify-between">
            <div className="flex items-center gap-2">
              <GripVertical className="text-gray-400" />
              <span>{m.name} (R{m.rank})</span>
            </div>
            <div className="flex items-center gap-1">
              <Trophy className="text-yellow-500" size={16} />
              <span>{m.wins}</span>
            </div>
          </Card>
        ))}
      </div>

      <div>
        <h2 className="text-xl font-bold mb-2">操作</h2>
        <Button onClick={shuffleTeams}>ランダムチーム分け</Button>
        <div className="mt-4">
          <Button onClick={() => handleWin('A')}>チームA勝利</Button>
          <Button className="ml-2" onClick={() => handleWin('B')}>チームB勝利</Button>
        </div>
      </div>

      <div>
        <h2 className="text-xl font-bold mb-2">チーム</h2>
        <div className="mb-4">
          <h3 className="font-semibold">チームA</h3>
          {teamA.map((m) => (
            <div key={m.name} className="bg-blue-100 p-2 rounded mb-1">{m.name} (R{m.rank})</div>
          ))}
        </div>
        <div>
          <h3 className="font-semibold">チームB</h3>
          {teamB.map((m) => (
            <div key={m.name} className="bg-red-100 p-2 rounded mb-1">{m.name} (R{m.rank})</div>
          ))}
        </div>
      </div>
    </div>
  );
}

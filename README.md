import React from "react";
import "./ComplexityCard.scss";

export type Variant = "green" | "red";

export interface RowData {
  fileName: string;
  complexity: string;
}

interface Props {
  title: string;
  variant: Variant;
  rows: RowData[];
  width?: number;
  height?: number;
}

const ComplexityCard: React.FC<Props> = ({
  title,
  variant,
  rows,
  width = 420,
  height = 270
}) => {
  return (
    <div className={`complexity-card ${variant}`} style={{ width, height }}>
      {/* Back layer: soft plate + right polygon stripe */}
      <div className="band" aria-hidden="true" />

      {/* Middle layer: white body (clips content) */}
      <div className="body">
        {/* Top layer: polygon header */}
        <div className="label">{title}</div>

        <div className="table-wrap">
          <table>
            <thead>
              <tr>
                <th>File name</th>
                <th>Complexity</th>
              </tr>
            </thead>
            <tbody>
              {rows.map((r, i) => (
                <tr key={`${r.fileName}-${i}`}>
                  <td>{r.fileName}</td>
                  <td>{r.complexity}</td>
                </tr>
              ))}
            </tbody>
          </table>
        </div>
      </div>
    </div>
  );
};

export default ComplexityCard;



:root{
  --green:#3abf6f;
  --green-soft:#e8f6ee;
  --red:#e65b53;
  --red-soft:#fdeceb;
  --card-radius:12px;
  --shadow:0 2px 10px rgba(0,0,0,.06);
  --border:#e6e6ea;
}

.complexity-card{
  position: relative;
  border-radius: var(--card-radius);
  font-family: Inter, Arial, sans-serif;

  /* BACK LAYER */
  .band{
    position:absolute;
    inset:0;
    border-radius:var(--card-radius);
    z-index:0;
    overflow:hidden;

    &::after{
      content:"";
      position:absolute;
      right:8px;
      top:8px;
      bottom:8px;
      width:34%;
      border-bottom-right-radius:var(--card-radius);
      border-bottom-left-radius:6px;
      clip-path: polygon(18% 0, 100% 0, 100% 100%, 0 100%, 0 16%);
      z-index:0;
    }
  }
  &.green .band{ background:var(--green-soft); }
  &.red   .band{ background:var(--red-soft); }
  &.green .band::after{ background:var(--green); }
  &.red   .band::after{ background:var(--red); }

  /* MIDDLE LAYER */
  .body{
    position:absolute;
    inset:10px;
    background:#fff;
    border:1px solid var(--border);
    border-radius:var(--card-radius);
    box-shadow:var(--shadow);
    z-index:1;
    overflow:hidden; /* CRITICAL: table stays inside white card */
  }

  /* TOP LAYER (attached to body) */
  .label{
    position:absolute;
    top:-12px;
    left:18px;
    height:44px;
    line-height:44px;
    padding:0 16px;
    color:#fff;
    font-weight:700;
    letter-spacing:.2px;
    border-radius:10px 10px 0 0;
    clip-path: polygon(0 0, 100% 0, 100% 78%, 86% 78%, 76% 100%, 0 100%);
    z-index:2;
  }
  &.green .label{ background:var(--green); }
  &.red   .label{ background:var(--red); }

  /* TABLE */
  .table-wrap{
    position:absolute;
    inset:44px 14px 14px 14px;
    overflow:auto;
  }
  table{ width:100%; border-collapse:collapse; }
  th, td{ background:#fff; font-size:14px; }
  thead th{
    text-align:left;
    padding:10px 10px;
    border-bottom:1px solid #e9e9ee;
    color:#333;
  }
  tbody td{
    padding:12px 10px;
    border-bottom:1px solid #f0f0f4;
    color:#444;
  }
  tbody tr:last-child td{ border-bottom:0; }
  th:first-child, td:first-child{ border-right:1px solid #efeff4; }
}







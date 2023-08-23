---
import BaseLayout from "../layouts/BaseLayout.astro";
import HorizontalCard from "../components/HorizontalCard.astro";
---

<BaseLayout title="Projects" sideBarActiveItemID="Stats">
  <div class="container">
    <div class="text-center">
      <h1><strong>Wall of achievements 🥳</strong></h1>
    </div>
    <table class="table">
      <thead>
        <tr>
          <th><strong>Overall issues</strong></th>
          <th><strong>High risk</strong></th>
          <th><strong>Unique highs</strong></th>
          <th><strong>Medium risk</strong></th>
          <th><strong>Unique mediums</strong></th>
          <th><strong>Projects audited</strong></th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>45</td>
          <td>14</td>
          <td>0</td>
          <td>26</td>
          <td>2</td>
          <td>17</td>
        </tr>
      </tbody>
    </table>

    <br />
    <br />
    <div class="text-center">
      <h1><strong>Sherlock</strong></h1>
    </div>
    <table class="table">
      <thead>
        <tr>
          <th>Contest</th>
          <th>High risk</th>
          <th>Medium risk</th>
          <th>Security report</th>
          <th>Payout</th>
          <th>Language</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Unstoppable</td>
          <td>3</td>
          <td>0</td>
          <td>-</td>
          <td>$1924.18</td>
          <td>Vyper</td>
        </tr>
        <tr>
          <td>Hubble-exchange</td>
          <td>0</td>
          <td>3 (1 solo)</td>
          <td>-</td>
          <td>$2,415.61</td>
          <td>Solidity</td>
        </tr>
        <tr>
          <td>Dodo</td>
          <td>-</td>
          <td>-</td>
          <td>-</td>
          <td>-</td>
          <td>Solidity</td>
        </tr>
        <tr>
          <td>Real-wagmi</td>
          <td>-</td>
          <td>-</td>
          <td>-</td>
          <td>-</td>
          <td>Solidity</td>
        </tr>
        <tr>
          <td>Index</td>
          <td>0</td>
          <td>5</td>
          <td>-</td>
          <td>$123.58</td>
          <td>Solidity</td>
        </tr>
        <tr>
          <td>Ironbank</td>
          <td>0</td>
          <td>4</td>
          <td>-</td>
          <td>$104.39</td>
          <td>Solidity</td>
        </tr>
        <tr>
          <td>USSD</td>
          <td>4</td>
          <td>5</td>
          <td>-</td>
          <td>$28.91</td>
          <td>Solidity</td>
        </tr>
        <tr>
          <td>Blueberry</td>
          <td>1</td>
          <td>1</td>
          <td>15</td>
          <td>$518.78</td>
          <td>Solidity</td>
        </tr>
      </tbody>
    </table>

    <br />
    <br />
    <div class="text-center">
      <h1><strong>Code4rena</strong></h1>
    </div>
    <table class="table">
      <thead>
        <tr>
          <th>Contest</th>
          <th>High risk</th>
          <th>Medium risk</th>
          <th>Security report</th>
          <th>Payout</th>
          <th>Language</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Asymmetry Finance</td>
          <td>2</td>
          <td>2</td>
          <td
            ><a href="https://code4rena.com/reports/2023-03-asymmetry">Report</a
            ></td
          >
          <td>$85.96</td>
          <td>Solidity</td>
        </tr>
        <tr>
          <td>Rubicon v2</td>
          <td>4</td>
          <td>2</td>
          <td>-</td>
          <td>$826.54</td>
          <td>Solidity</td>
        </tr>
        <tr>
          <td>Venus Protocol Isolated Pools</td>
          <td>-</td>
          <td>1</td>
          <td>-</td>
          <td>$732.00</td>
          <td>Solidity</td>
        </tr>
        <tr>
          <td>Maia DAO Ecosystem</td>
          <td>-</td>
          <td>2</td>
          <td>-</td>
          <td>$24.76</td>
          <td>Solidity</td>
        </tr>
        <tr>
          <td>Lybra Finance</td>
          <td>-</td>
          <td>1 (solo)</td>
          <td>-</td>
          <td>$1,444.45</td>
          <td>Solidity</td>
        </tr>
        <tr>
          <td>Amphora Protocol</td>
          <td>-</td>
          <td>-</td>
          <td>-</td>
          <td>-</td>
          <td>Solidity</td>
        </tr>
        <tr>
          <td>Arcade.xyz</td>
          <td>-</td>
          <td>-</td>
          <td>-</td>
          <td>-</td>
          <td>Solidity</td>
        </tr>
      </tbody>
    </table>

    <br />
    <br />
    <!-- ... CodeHawks table ... -->
    <div class="text-center">
      <h1><strong>CodeHawks</strong></h1>
    </div>
    <table class="table">
      <thead>
        <tr>
          <th>Contest</th>
          <th>High risk</th>
          <th>Medium risk</th>
          <th>Security report</th>
          <th>Payout</th>
          <th>Language</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Beedle</td>
          <td>-</td>
          <td>-</td>
          <td>-</td>
          <td>-</td>
          <td>Solidity</td>
        </tr>
      </tbody>
    </table>

    <br />
    <br />
    <div class="text-center">
      <h1 class="mb-4 font-weight-bold">Solo Issues</h1>
    </div>
    <ul class="list-unstyled">
      <li>
        <a
          href="https://github.com/code-423n4/2023-06-lybra-findings/issues/484"
          class="text-primary">Issue 1</a
        >
      </li>
      <li>
        <a
          href="https://github.com/sherlock-audit/2023-04-hubble-exchange-judging/issues/234"
          class="text-primary">Issue 2</a
        >
      </li>
    </ul>
  </div>

  <style>
    /* Add the following CSS to style the links */
    .text-primary {
      color: white;
    }
  </style>
</BaseLayout>
